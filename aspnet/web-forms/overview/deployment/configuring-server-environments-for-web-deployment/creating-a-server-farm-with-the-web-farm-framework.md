---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: Vytvoření serverové farmy pomocí rozhraní Web farme | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak používat WFF (Web Farm Framework) 2,0 k vytvoření a konfiguraci farmy webových serverů z kolekce serverů.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: 204996514bed336e60ab77f184a923f04e7e2bba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637247"
---
# <a name="creating-a-server-farm-with-the-web-farm-framework"></a>Vytvoření serverové farmy na platformě Web Farm Framework

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak používat WFF (Web Farm Framework) 2,0 k vytvoření a konfiguraci farmy webových serverů z kolekce serverů.

WFF umožňuje synchronizovat produkty a součásti webové platformy, webové aplikace, weby a nastavení konfigurace na více webových serverech s vyrovnáváním zatížení. Ve scénářích, kdy potřebujete více než jeden webový server, jako jsou pracovní a produkční prostředí, může to značně zjednodušit proces nasazení a konfigurace. Webovou aplikaci můžete nasadit na jeden server&#x2014;. *primární server*&#x2014;a WFF automaticky replikují tuto webovou aplikaci na všechny ostatní webové servery v serverové farmě.

## <a name="understanding-the-web-farm-framework"></a>Principy rozhraní Web farme

WFF 2,0 můžete použít k zřizování, správě a nasazování obsahu do skupiny webových serverů. Nasazení WFF se skládá ze tří klíčových rolí serveru:

- *Server řadiče*. Pomocí tohoto serveru vytvoříte a nakonfigurujete serverové farmy WFF. Server řadiče spravuje synchronizaci komponent webové platformy, nastavení konfigurace a aplikací mezi webovými servery v serverové farmě. Na server kontroléru nainstalujete WFF 2,0 a server kontroleru pak na každý ze serverů v serverové farmě nainstaluje agenta WFF. Server kontroléru nepatří do žádné serverové farmy WFF a jeden server s jedním řadičem může spravovat více serverových farem. V tomto scénáři použijete jeden server WFF Controller k vytvoření a správě pracovní farmy a provozní serverové farmy.
- *Primární server*. Každá WFF serverová farma zahrnuje jeden primární server. Když nainstalujete komponenty webové platformy nebo nasadíte aplikace na primární server, WFF synchronizuje vaše změny na všech ostatních serverech v serverové farmě.
- *Sekundární server*. Každá WFF serverová farma obsahuje jeden nebo více sekundárních serverů. Všechny změny, které provedete na primárním serveru, se replikují na všechny sekundární servery v serverové farmě.

To ukazuje, jak se tyto role serveru vztahují k prostředím Fabrikam, Inc. a produkčním prostředím:

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

V tomto scénáři se přípravné prostředí a provozní prostředí nakonfigurují jak na WFF serverové farmy. Jeden server WFF Controller spravuje obě farmy. V rámci každé serverové farmy jsou všechny změny primárního serveru replikovány na všechny sekundární servery.

Než začnete konfigurovat pracovní a produkční prostředí, doporučujeme si přečtěte si tyto články, abyste se seznámili se základními koncepty WFF 2,0:

- [Přehled rozhraní Web farme Framework 2,0 pro službu IIS 7](https://go.microsoft.com/?linkid=9805126)
- [Nastavení serverové farmy s webovým rozhraním web farme 2,0 pro IIS 7](https://go.microsoft.com/?linkid=9805127)
- [Požadavky na systém a platformu pro webovou farmu rozhraní 2,0 pro IIS 7](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a>Přehled úlohy

Chcete-li dokončit úlohy a návody v tomto tématu, budete potřebovat alespoň tři servery&#x2014;jeden řadič WFF, jeden primární webový server pro serverovou farmu a jeden nebo více sekundárních webových serverů pro serverovou farmu. K serverové farmě WFF můžete kdykoli přidat další sekundární servery. Pokud chcete vytvořit a nakonfigurovat farmu WFF serveru pro své pracovní nebo produkční prostředí, musíte na nejvyšší úrovni:

- Vytvořte server kontroléru instalací Internetová informační služba (IIS) 7,5 a WFF 2,0.
- Primární a sekundární servery Připravte vytvořením běžného účtu správce a konfigurací výjimek brány firewall.
- Nakonfigurujte serverovou farmu pomocí Správce služby IIS na serveru kontroleru.
- Nakonfigurujte vyrovnávání zatížení pomocí funkce směrování požadavků aplikace IIS nebo alternativním technologií vyrovnávání zatížení.

V úlohách a návodech v tomto tématu se předpokládá, že začínáte s čistým sestavením serveru se systémem Windows Server 2008 R2. Než začnete, ověřte u každého serveru, že:

- Nainstaluje se Windows Server 2008 R2 Service Pack 1 a nainstalují se všechny dostupné aktualizace.
- Server je připojený k doméně.
- Server má statickou IP adresu.

> [!NOTE]
> Další informace o připojení počítačů k doméně najdete v tématu [připojení počítačů k doméně a přihlášení](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx). Další informace o konfiguraci statických IP adres najdete v tématu [Konfigurace statické IP adresy](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).

## <a name="create-the-wff-controller-server"></a>Vytvoření serveru WFF Controller

Pokud chcete vytvořit server WFF Controller, budete muset nainstalovat IIS 7 nebo novější a WFF 2,0 nebo novější. V rámci pokrývá WFF používá nástroj pro nasazení webu služby IIS (Nasazení webu) 2. x k synchronizaci serverů ve farmě. Použijete-li k instalaci WFF instalační program webové platformy, instalační program bude automaticky stahovat a instalovat Nasazení webu.

**Vytvoření serveru WFF Controller**

1. Stáhněte a nainstalujte [instalační program webové platformy](https://go.microsoft.com/?linkid=9739157).
2. V horní části okna **Instalace webové platformy 3,0** klikněte na **produkty**.
3. Na levé straně okna klikněte v navigačním podokně na možnost **Server**.
4. V řádku **Konfigurace doporučeného pro IIS 7** klikněte na **Přidat**.
5. Ve <strong>webové farmě Framework 2.</strong> <em>x</em> řádek, klikněte na tlačítko <strong>Přidat</strong>.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. Klikněte na **Nainstalovat**. Všimněte si, že instalační program webové platformy přidal do seznamu instalace Nástroj pro nasazení webu společně s různými dalšími závislostmi.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. Přečtěte si licenční podmínky a pokud souhlasíte s podmínkami **, klikněte na Souhlasím.**
8. Po dokončení instalace klikněte na **Dokončit**a potom zavřete okno **instalace webové platformy 3,0** .

## <a name="configure-the-primary-and-secondary-servers"></a>Konfigurace primárních a sekundárních serverů

Před vytvořením serverové farmy WFF byste měli provést některé přípravné úkoly na webových serverech, které tvoří farmu:

- Přidáním výjimek brány firewall umožníte, aby **základní síťové**funkce, **Vzdálená správa**a funkce **sdílení souborů a tiskáren** komunikovaly se serverem WFF Controller.
- Vytvořte účet domény (například **FABRIKAM\stagingfarm**) ve službě Active Directory a přidejte ho do místní skupiny Administrators na každém serveru. Tento účet použijete jako účet správce serverové farmy při vytváření serverové farmy.

Další informace o tom, jak nakonfigurovat tyto výjimky brány firewall v bráně Windows Firewall, najdete v tématu [požadavky na systém a platformu pro webovou farmu rozhraní 2,0 pro službu IIS 7](https://go.microsoft.com/?linkid=9805128). Další systémy brány firewall najdete v dokumentaci k produktu.

Následující postup můžete použít k přidání účtu domény do skupiny místních správců v systému Windows Server 2008 R2. Tento postup byste měli provést na každém serveru, který chcete přidat k serverové farmě&#x2014;jinými slovy, přidejte stejný účet domény do místní skupiny Administrators na primárním serveru a na každém sekundárním serveru.

**Přidání účtu domény do místní skupiny Administrators**

1. V nabídce **Start** přejděte na **Nástroje pro správu**a potom klikněte na **Správce serveru**.
2. V okně **Správce serveru** v podokně stromové zobrazení rozbalte položku **Konfigurace**, rozbalte položku **místní uživatelé a skupiny**a potom klikněte na možnost **skupiny**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. V podokně **skupiny** poklikejte na **správce**.
4. V dialogovém okně **vlastnosti správců** klikněte na tlačítko **Přidat**.
5. V dialogovém okně **Vybrat uživatele, počítače, účty služby nebo skupiny** zadejte (nebo přejděte) k účtu domény (například **FABRIKAM\stagingfarm**) a pak klikněte na **OK**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. V dialogovém okně **vlastnosti správců** klikněte na tlačítko **OK**.

Vaše servery jsou teď připravené k přidání do serverové farmy. V případě primárního serveru můžete server nakonfigurovat tak, aby splňoval požadavky vaší aplikace před nebo po vytvoření serverové farmy&#x2014;v obou případech, WFF provede synchronizaci serverů nasazením stejných produktů, součástí nebo konfigurací do sekundárních serverů. V zájmu zjednodušení tento kurz předpokládá, že po dokončení vytváření serverové farmy nakonfigurujete primární server.

## <a name="create-the-wff-server-farm"></a>Vytvoření serverové farmy WFF

V tuto chvíli jsou všechny servery připravené k přidání do serverové farmy WFF:

- Nainstalovali jste WFF na server řadiče.
- Na primárních a sekundárních webových serverech jste nakonfigurovali výjimky brány firewall.
- Přidali jste účet domény do místní skupiny Administrators na primárních a sekundárních webových serverech.

Dalším krokem je vytvoření serverové farmy v WFF. To můžete provést ze Správce služby IIS na serveru kontroleru WFF.

**Vytvoření serverové farmy WFF**

1. Na serveru řadiče WFF v nabídce **Start** přejděte na **Nástroje pro správu**a potom Internetová informační služba klikněte na **Správce služby IIS**.
2. V podokně **připojení** rozbalte uzel místní server, klikněte pravým tlačítkem na **serverové farmy**a pak klikněte na **vytvořit serverovou farmu**.
3. V dialogovém okně **vytvořit serverovou farmu** zadejte smysluplný název serverové farmy (například **pracovní farmu**) a pak vyberte **zřídit serverovou farmu**.
4. Zadejte uživatelské jméno a heslo účtu domény, který jste přidali do skupiny místních správců na jednotlivých serverech.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. Klikněte na **Další**.
6. Na stránce **Přidat servery** zadejte plně kvalifikovaný název domény (FQDN) primárního serveru, vyberte **primární server**a pak klikněte na **Přidat**.
7. V tomto okamžiku se WFF pokusí kontaktovat primární server pomocí zadaných přihlašovacích údajů. Pokud je připojení úspěšné, primární server se přidá do tabulky na stránce **Přidat servery** .

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > Možná jste si všimli, že **Server je dostupný pro vyrovnávání zatížení** , který je ve výchozím nastavení vybraný. WFF používá modul IIS ARR k implementaci vyrovnávání zatížení, a proto distribuuje požadavky napříč webovými servery v serverové farmě. Ve většině scénářů byste měli jenom zrušit možnost, že **Server je dostupný pro vyrovnávání zatížení** , pokud jste místo toho chtěli použít řešení vyrovnávání zatížení od jiného výrobce.
8. Na stránce **Přidat servery** zadejte plně kvalifikovaný název domény prvního sekundárního serveru a pak klikněte na **Přidat**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. Opakujte krok 7 u všech dalších sekundárních serverů ve farmě a potom klikněte na tlačítko **Dokončit**.

Vaše serverová farma WFF je teď v provozu. Všechny produkty nebo komponenty webové platformy, které nainstalujete na primární server, a všechny webové aplikace nebo obsah, které nasadíte na primární server, budou automaticky zřízeny na všech vašich sekundárních serverech.

WFF je široké a složité téma. Další informace o tom najdete na webu [Microsoft Web Farm Framework 2,0 pro IIS 7](https://go.microsoft.com/?linkid=9805129) . V tuto chvíli ale existují dvě oblasti funkcí, o kterých byste měli vědět:

- *Zřizování aplikací* je proces, který replikuje obsah z primárního serveru, jako jsou webové aplikace a nastavení konfigurace, napříč všemi sekundárními servery v serverové farmě. Pokud například nasadíte ukázkové řešení Contact Manageru na váš primární pracovní server, proces zřizování aplikace WFF toto řešení nasadí na všechny sekundární pracovní servery. Ve výchozím nastavení se proces zřizování aplikace spouští každých 30 sekund.
- *Zřizování platformy* je proces, který synchronizuje produkty a součásti webové platformy z primárního serveru na všechny sekundární servery v serverové farmě. Pokud například nainstalujete ASP.NET MVC 3 na primární pracovní server, proces zřizování platformy použije instalační program webové platformy k instalaci ASP.NET MVC 3 na všechny sekundární pracovní servery. Ve výchozím nastavení se proces zřizování platformy spouští každých pět minut.

Základní nastavení pro zřizování aplikací a platforem můžete spravovat pomocí Správce služby IIS na serveru WFF Controller.

**Prozkoumat nastavení zřizování aplikací a platforem**

1. Ve Správci služby IIS vyberte v podokně **připojení** svou serverovou farmu.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. V podokně **Serverová farma** poklikejte na **zřizování aplikací**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. Jak vidíte, je serverová farma momentálně nakonfigurovaná tak, aby synchronizoval webový obsah a konfigurační nastavení mezi primárním serverem a sekundárními servery každých 30 sekund.
4. Klikněte na **back (zpět**) a potom poklikejte na **zřizování platforem**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. Jak vidíte, je serverová farma momentálně nakonfigurovaná tak, aby synchronizoval produkty a součásti webových platforem mezi primárním serverem a sekundárními servery každých pět minut.
6. Klikněte na tlačítko **zpět**.
7. Chcete-li vynutit, aby serverová farma ihned synchronizoval produkty webové platformy, klikněte v podokně **Akce** na možnost **zřídit platformu**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > Zřizování platformy může nějakou dobu trvat. Proces instalačního programu běží na pozadí na sekundárních serverech v serverové farmě.
8. Až zadáte dostatek času na dokončení procesu zřizování, můžete ověřit, zda byly produkty a součásti přidané na primární server nyní replikovány na sekundárních serverech. Můžete se například přihlásit k sekundárnímu serveru a pomocí okna **Správce serveru** ověřit, zda byla role webového serveru nainstalována.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. Můžete také zkontrolovat seznam nainstalovaných programů a ověřit, zda byly přidány různé komponenty webové platformy.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a>Konfigurace vyrovnávání zatížení

Když vytváříte webovou farmu, musíte nastavit určitou formu vyrovnávání zatížení pro distribuci požadavků HTTP mezi webovými servery. Může se jednat o řešení vyrovnávání zatížení sítě Windows Server 2008, službu IIS ARR nebo softwarové nebo hardwarové vyrovnávání zatížení založené na hardwaru.

WFF je navržená tak, aby úzce spolupracuje se službou IIS ARR. Chcete-li využít výhod této integrace, je nutné nainstalovat modul ARR na server řadiče WFF. Pak nasměrujete veškerý webový provoz na server kontroléru, obvykle konfigurací záznamů DNS (Domain Name System). Server řadiče pak bude distribuovat příchozí požadavky mezi servery ve vaší farmě na základě dostupnosti serveru a dalších dalších kritérií.

> [!NOTE]
> Nemusíte používat ARR s WFF; WFF můžete nakonfigurovat tak, aby fungovala s řešeními vyrovnávání zatížení třetích stran. Další informace najdete v tématu [Přehled webové farmy rozhraní 2,0 pro službu IIS 7](https://go.microsoft.com/?linkid=9805126).

Vyrovnávání zatížení pomocí ARR je složité téma, většinu z nich je nad rámec tohoto kurzu. Pomocí následujícího postupu však můžete nainstalovat modul ARR a začít s vyrovnáváním zatížení.

**Nastavení vyrovnávání zatížení na serveru WFF Controller**

1. Na serveru řadiče WFF spusťte instalační program webové platformy.
2. V horní části okna **Instalace webové platformy 3,0** klikněte na **produkty**.
3. Na levé straně okna klikněte v navigačním podokně na možnost **Server**.
4. V řádku **Směrování žádostí o aplikace 2,5** klikněte na **Přidat**.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. Klikněte na **nainstalovat**a pak postupujte podle pokynů v okně **Instalace webové platformy** .
6. Po dokončení instalace spusťte Správce služby IIS a v podokně **připojení** klikněte na uzel serverová farma. Všimněte si, že v podokně **serverové farmy** byly přidány některé nové ikony.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. V podokně **Serverová farma** dvakrát klikněte na **Vyrovnávání zatížení**.
8. V podokně **Vyrovnávání zatížení** vyberte algoritmus vyrovnávání zatížení (například **nejméně aktuální požadavek**).

    > [!NOTE]
    > Další informace o algoritmech vyrovnávání zatížení a dalších nastaveních konfigurace najdete v tématu [modul směrování žádostí o aplikace](https://go.microsoft.com/?linkid=9805130).

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. V podokně **Akce** klikněte na **Použít**.

Nyní jste nakonfigurovali základní vyrovnávání zatížení pro servery v serverové farmě. Pokud nasměrujete veškerý provoz webové farmy na server kontroléru, požadavky budou distribuovány mezi servery ve vaší farmě podle dostupnosti a vybraného algoritmu vyrovnávání zatížení.

Další informace o tom, jak nakonfigurovat vyrovnávání zatížení pomocí ARR, najdete v tématu [modul směrování žádostí o aplikace](https://go.microsoft.com/?linkid=9805130).

## <a name="monitor-the-server-farm"></a>Monitorování serverové farmy

Stav serverové farmy můžete monitorovat kdykoli prostřednictvím Správce služby IIS na serveru řadiče. V podokně **připojení** rozbalte serverovou farmu a potom klikněte na **servery**. V prostředním podokně se zobrazí souhrn všech serverů ve farmě společně s protokolem trasování nedávné aktivity.

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a>Závěr

Vaše serverová farma WFF by teď měla být spuštěná. Primární server můžete nakonfigurovat tak, aby podporoval&#x2014;&#x2014;i libovolný přístup k nasazení. upřednostňujete si další část pro čtení a vaše konfigurace bude replikována na každém sekundárním serveru v serverové farmě.

## <a name="further-reading"></a>Další čtení

Další informace o všech aspektech konfigurace a používání služby WFF najdete na webu [Microsoft Web Farm Framework 2,0 pro IIS 7](https://go.microsoft.com/?linkid=9805129) .

> [!div class="step-by-step"]
> [Předchozí](configuring-a-database-server-for-web-deploy-publishing.md)
> [Další](configuring-deployment-properties-for-a-target-environment.md)
