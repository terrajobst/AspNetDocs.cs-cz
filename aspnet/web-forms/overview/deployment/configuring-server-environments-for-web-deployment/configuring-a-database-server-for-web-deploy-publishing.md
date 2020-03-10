---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: Konfigurace databázového serveru pro Nasazení webu publikování | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak nakonfigurovat databázový server SQL Server 2008 R2 pro podporu nasazení a publikování webu. Úkoly popsané v tomto tématu jsou společně...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: ade3c1ba1c470092f512436f39b8831458408c2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634615"
---
# <a name="configuring-a-database-server-for-web-deploy-publishing"></a>Konfigurace databázového serveru pro publikování nasazeného webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak nakonfigurovat databázový server SQL Server 2008 R2 pro podporu nasazení a publikování webu.
> 
> Úkoly popsané v tomto tématu jsou společné pro každý scénář&#x2014;nasazení. nezáleží na tom, jestli jsou webové servery nakonfigurované tak, aby používaly službu vzdáleného agenta nástroje pro nasazení webu IIS (nasazení webu), obslužná rutina nasazení webu nebo online nasazení nebo vaše aplikace je spuštěná na jednom webovém serveru nebo v serverové farmě. Způsob, jakým nasazujete databázi, se může změnit v závislosti na požadavcích na zabezpečení a dalších ohledech. Například můžete nasadit databázi s ukázkovými daty nebo bez nich a můžete nasazovat mapování rolí uživatelů nebo je nakonfigurovat ručně po nasazení. Způsob konfigurace databázového serveru však zůstává stejný.

Není nutné instalovat žádné další produkty ani nástroje pro konfiguraci databázového serveru pro podporu nasazení webu. Za předpokladu, že váš databázový server a webový server běží v různých počítačích, stačí:

- Povolí SQL Server komunikaci pomocí protokolu TCP/IP.
- Povolí SQL Server provoz přes jakékoli brány firewall.
- Udělte účtu počítače webového serveru SQL Server přihlášení.
- Namapujte přihlašovací údaje účtu počítače na všechny požadované databázové role.
- Udělte účtu, který spustí nasazení, oprávnění SQL Server přihlášení a tvůrce databáze.
- Pokud chcete podporu zopakovat, namapujte přihlašovací údaje účtu nasazení na roli databáze role **vlastníka\_** databáze.

V tomto tématu se dozvíte, jak provádět jednotlivé postupy. V úlohách a návodech v tomto tématu se předpokládá, že začínáte s výchozí instancí SQL Server 2008 R2 spuštěnou v systému Windows Server 2008 R2. Než budete pokračovat, ujistěte se, že:

- Nainstaluje se Windows Server 2008 R2 Service Pack 1 a nainstalují se všechny dostupné aktualizace.
- Server je připojený k doméně.
- Server má statickou IP adresu.
- Nainstalují se SQL Server 2008 R2 Service Pack 1 a všechny dostupné aktualizace.

Instance SQL Server musí zahrnovat jenom roli **služby databázového stroje** , která je zahrnutá automaticky v jakékoli SQL Server instalaci. Pro usnadnění konfigurace a údržby však doporučujeme, abyste zahrnuli **Nástroje pro správu – základní** a **Nástroje pro správu – úplné** role serveru.

> [!NOTE]
> Další informace o připojení počítačů k doméně najdete v tématu [připojení počítačů k doméně a přihlášení](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx). Další informace o konfiguraci statických IP adres najdete v tématu [Konfigurace statické IP adresy](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx). Další informace o instalaci SQL Server najdete v tématu [instalace SQL Server 2008 R2](https://technet.microsoft.com/library/bb500395.aspx).

## <a name="enable-remote-access-to-sql-server"></a>Povolit vzdálený přístup k SQL Server

SQL Server používá ke komunikaci se vzdálenými počítači protokol TCP/IP. Pokud je váš databázový server a webový server na různých počítačích, musíte:

- Nakonfigurujte nastavení SQL Server sítě tak, aby umožňovalo komunikaci přes protokol TCP/IP.
- Nakonfigurujte libovolné hardwarové nebo softwarové brány firewall tak, aby umožňovaly přenosy TCP (a v některých případech přenosy UDP (User Datagram Protocol)) na portech, které používá instance SQL Server.

Pokud chcete povolit SQL Server komunikaci přes protokol TCP/IP, změňte konfiguraci sítě pro instanci SQL Server pomocí SQL Server Configuration Manager.

**Povolení komunikace SQL Server pomocí protokolu TCP/IP**

1. V nabídce **Start** přejděte na **všechny programy**, klikněte na **Microsoft SQL Server 2008 R2**, klikněte na **konfigurační nástroje**a pak klikněte na **SQL Server Configuration Manager**.
2. V podokně stromové zobrazení rozbalte **SQL Server konfigurace sítě**a potom klikněte na **protokoly pro MSSQLSERVER**.

   > [!NOTE]
   > Pokud jste nainstalovali více instancí SQL Server, zobrazí se pro každou instanci <strong>protokol pro</strong>položku<em>[název instance]</em> . Nastavení sítě je třeba nakonfigurovat na základě instance.
3. V podokně podrobností klikněte pravým tlačítkem na řádek **TCP/IP** a pak klikněte na **Povolit**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. V dialogovém okně **Upozornění** klikněte na tlačítko **OK**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. Aby se nová konfigurace sítě projevila, musíte restartovat službu MSSQLSERVER. Můžete to provést z příkazového řádku, z konzoly služby nebo z SQL Server Management Studio. V tomto postupu použijete SQL Server Management Studio.
6. Zavřete SQL Server Configuration Manager.
7. V nabídce **Start** přejděte na **všechny programy**, klikněte na **Microsoft SQL Server 2008 R2**a potom klikněte na **SQL Server Management Studio**.
8. V dialogovém okně **připojit k serveru** zadejte do pole **název serveru** název databázového serveru a pak klikněte na **připojit**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. V podokně **Průzkumník objektů** klikněte pravým tlačítkem myši na uzel nadřazeného serveru (například **TESTDB1**) a pak klikněte na **restartovat**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. V dialogovém okně **Microsoft SQL Server Management Studio** klikněte na tlačítko **Ano**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. Po restartování služby ukončete SQL Server Management Studio.

Abyste povolili SQL Server provoz přes bránu firewall, musíte nejdřív zjistit, které porty vaše SQL Server instance používá. Bude záviset na tom, jak byla instance SQL Server vytvořená a nakonfigurovaná:

- *Výchozí instance* SQL Server naslouchá požadavkům (a reaguje na požadavky) na portu TCP 1433.
- *Pojmenovaná instance* SQL Server naslouchá požadavkům (a reaguje na) na dynamicky přiřazený port TCP.
- Pokud je povolená služba SQL Server Browser, klienti se můžou dotázat na službu na portu UDP 1434 a zjistit, který port TCP se má použít pro konkrétní instanci SQL Server. Z bezpečnostních důvodů je však tato služba často zakázána.

Za předpokladu, že používáte výchozí instanci SQL Server, musíte bránu firewall nakonfigurovat tak, aby umožňovala provoz.

| Směr | Z portu | Na port | Typ portu |
| --- | --- | --- | --- |
| Příchozí | Všechny | 1433 | TCP |
| Odchozí | 1433 | Všechny | TCP |

> [!NOTE]
> Technicky, klientský počítač bude používat náhodně přiřazený port TCP mezi 1024 a 5000 ke komunikaci s SQL Server a pravidla brány firewall můžete omezit odpovídajícím způsobem. Další informace o portech SQL Server a branách firewall najdete v tématu [čísla portů TCP/IP, která jsou nutná ke komunikaci do SQL přes bránu firewall](https://go.microsoft.com/?linkid=9805125) a [Postupy: Konfigurace serveru pro naslouchání na specifickém portu TCP (SQL Server Configuration Manager)](https://msdn.microsoft.com/library/ms177440.aspx).

Ve většině prostředí se systémem Windows Server bude pravděpodobně nutné nakonfigurovat bránu Windows Firewall na databázovém serveru. Brána Windows Firewall ve výchozím nastavení umožňuje všechny odchozí přenosy, pokud je pravidlo výslovně nezakáže. Chcete-li webovému serveru povolit přístup k vaší databázi, je nutné nakonfigurovat příchozí pravidlo, které umožňuje provoz TCP na čísle portu, které používá instance SQL Server. Pokud používáte výchozí instanci SQL Server, můžete toto pravidlo nakonfigurovat pomocí následujícího postupu.

**Konfigurace brány Windows Firewall tak, aby povolovala komunikaci s výchozí instancí SQL Server**

1. Na databázovém serveru, v nabídce **Start** , přejděte na **Nástroje pro správu**a pak klikněte na **Brána Windows Firewall s pokročilým zabezpečením**.
2. V podokně stromové zobrazení klikněte na **příchozí pravidla**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. V podokně **Akce** klikněte v části **příchozí pravidla**na **nové pravidlo**.
4. V Průvodci vytvořením nového příchozího pravidla na stránce **Typ pravidla** vyberte **port**a pak klikněte na **Další**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. Na stránce **protokol a porty** zkontrolujte, že je vybraná možnost **TCP** , a do pole **konkrétní místní porty** zadejte **1433**a potom klikněte na **Další**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. Na stránce **Akce** ponechejte políčko pro **Povolení připojení** zaškrtnuto a klikněte na **Další**.
7. Na stránce **profil** ponechte vybranou možnost **doména** , zrušte zaškrtnutí políček **privátní** a **veřejné** a potom klikněte na tlačítko **Další**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. Na stránce **název** uveďte pravidlo s vhodně popisným názvem (například **SQL Server výchozí instance – přístup k síti**) a pak klikněte na **Dokončit**.

Další informace o konfiguraci brány Windows Firewall pro SQL Server, zejména pokud potřebujete komunikovat s SQL Server přes nestandardní nebo dynamické porty, najdete v tématu [How to: Configure a brána Windows Firewall pro přístup k databázovému stroji](https://technet.microsoft.com/library/ms175043.aspx).

## <a name="configure-logins-and-database-permissions"></a>Konfigurace přihlašovacích údajů a oprávnění databáze

Když nasadíte webovou aplikaci na Internetová informační služba (IIS), aplikace se spustí s identitou fondu aplikací. V doménovém prostředí používají identity fondu aplikací účet počítače serveru, na kterém jsou spuštěny pro přístup k síťovým prostředkům. Účty počítačů mají ve formátu <em>[název domény]</em><strong>\</strong ><em>[název počítače]</em> <strong>$</strong> &#x2014;například <strong>FABRIKAM\TESTWEB1 $</strong>. Chcete-li webové aplikaci dovolit přístup k databázi v síti, je třeba:

- Přidejte přihlášení k účtu počítače webového serveru do instance SQL Server.
- Namapujte přihlašovací údaje účtu počítače na všechny požadované databázové role (obvykle **db\_DataReader** a **DB\_datawrite**).

Pokud je webová aplikace spuštěna na serverové farmě, nikoli na jednom serveru, budete muset tyto postupy opakovat pro každý webový server v serverové farmě.

> [!NOTE]
> Další informace o identitách fondu aplikací a přístupu k síťovým prostředkům najdete v tématu [identity fondů aplikací](https://go.microsoft.com/?linkid=9805123).

K těmto úlohám se můžete přiblíží různými způsoby. Chcete-li vytvořit přihlašovací údaje, můžete:

- Ruční vytvoření přihlašovacích údajů na databázovém serveru pomocí jazyka Transact-SQL nebo SQL Server Management Studio.
- K vytvoření a nasazení přihlášení použijte projekt serveru SQL Server 2008 v aplikaci Visual Studio.

Přihlášení SQL Server je objekt na úrovni serveru, nikoli objekt na úrovni databáze, takže není závislý na databázi, kterou chcete nasadit. V takovém případě můžete vytvořit přihlášení kdykoli a nejjednodušší způsob, jak ručně vytvořit přihlašovací údaje na databázovém serveru, než začnete s nasazováním databází. Pomocí následujícího postupu můžete vytvořit přihlášení v SQL Server Management Studio.

**Vytvoření přihlášení SQL Server pro účet počítače webového serveru**

1. Na databázovém serveru přejděte v nabídce **Start** na položku **všechny programy**, klikněte na **Microsoft SQL Server 2008 R2**a pak klikněte na **SQL Server Management Studio**.
2. V dialogovém okně **připojit k serveru** zadejte do pole **název serveru** název databázového serveru a pak klikněte na **připojit**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. V podokně **Průzkumník objektů** klikněte pravým tlačítkem na **zabezpečení**, přejděte na **Nový**a pak klikněte na **Přihlásit**.
4. V dialogovém okně **přihlášení – nové** zadejte do pole **přihlašovací jméno** název vašeho účtu počítače webového serveru (například **FABRIKAM\TESTWEB1 $** ).

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. Klikněte na tlačítko **OK**.

V tomto okamžiku je váš databázový server připravený na Nasazení webu publikování. Řešení, která nasazujete, ale nebudou fungovat, dokud nemapujete přihlášení účtu počítače k požadovaným databázovým rolím. Mapování přihlašovacích údajů k databázovým rolím vyžaduje mnohem více, protože role nemůžete mapovat, dokud nebudete databázi nasazovat. Pokud chcete mapovat přihlašovací údaje účtu počítače k požadovaným databázovým rolím, můžete:

- Po prvním nasazení databáze přiřaďte databázové role k přihlašovacímu jménu ručně.
- K přiřazení databázových rolí k přihlašování použijte skript po nasazení.

Další informace o automatizaci vytváření přihlašovacích údajů a mapování databázových rolí najdete v tématu [nasazení členství databázové role do testovacích prostředí](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md). Případně můžete použít další postup k mapování přihlašovacích údajů účtu počítače k požadovaným databázovým rolím ručně. Mějte na paměti, že tento postup nemůžete provést až *po* nasazení databáze.

**Mapování databázových rolí na přihlašovací údaje účtu počítače webového serveru**

1. Otevřete SQL Server Management Studio jako dříve.
2. V podokně **Průzkumník objektů** rozbalte uzel **zabezpečení** , rozbalte uzel **přihlášení** a potom poklikejte na přihlašovací jméno účtu počítače (například **FABRIKAM\TESTWEB1 $** ).

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. V dialogovém okně **Vlastnosti přihlášení** klikněte na **mapování uživatelů**.
4. V poli **Uživatelé namapované na tuto tabulku přihlášení** vyberte název vaší databáze (například **ContactManager**).
5. V seznamu **členství databázové role pro:** *[název databáze]* vyberte požadovaná oprávnění. V případě ukázkového řešení Contact Manager je nutné vybrat role **db\_DataReader** a **DB\_datawrite** .

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. Klikněte na tlačítko **OK**.

Zatímco ruční mapování databázových rolí je často více než adekvátní pro testovací prostředí, je méně žádoucí pro automatizovaná nasazení nebo nasazení jedním kliknutím do pracovních nebo produkčních prostředí. Další informace o automatizaci tohoto typu úlohy pomocí skriptů po nasazení najdete v části [nasazení členství databázové role do testovacích prostředí](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).

> [!NOTE]
> Další informace o serverových projektech a databázových projektech naleznete v tématu [Visual Studio 2010 SQL Server Database Projects](https://msdn.microsoft.com/library/ff678491.aspx).

## <a name="configure-permissions-for-the-deployment-account"></a>Konfigurace oprávnění pro účet nasazení

Pokud účet, který použijete ke spuštění nasazení, není správcem SQL Server, budete také muset vytvořit přihlašovací údaje pro tento účet. Aby bylo možné databázi vytvořit, musí být tento účet členem role serveru **dbcreator** nebo mít ekvivalentní oprávnění.

> [!NOTE]
> Když k nasazení databáze použijete Nasazení webu nebo VSDBCMD, můžete použít přihlašovací údaje systému Windows nebo přihlašovací údaje SQL Server (Pokud je vaše instance SQL Server nakonfigurovaná tak, aby podporovala ověřování ve smíšeném režimu). Další postup předpokládá, že chcete použít přihlašovací údaje pro Windows, ale při konfiguraci nasazení se nezastavíte tím, že v připojovacím řetězci zabráníte zadání SQL Server uživatelského jména a hesla.

**Nastavení oprávnění pro účet nasazení**

1. Otevřete SQL Server Management Studio jako dříve.
2. V podokně **Průzkumník objektů** klikněte pravým tlačítkem na **zabezpečení**, přejděte na **Nový**a pak klikněte na **Přihlásit**.
3. V dialogovém okně **přihlášení – nové** zadejte do pole **přihlašovací jméno** název vašeho účtu nasazení (například **FABRIKAM\matt**).
4. V podokně **Vybrat stránku** klikněte na **role serveru**.
5. Vyberte **dbcreator**a pak klikněte na **OK**.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

Aby bylo možné podporovat následná nasazení, budete také muset po prvním nasazení přidat účet nasazení do role **vlastníka\_** databáze. Důvodem je to, že při následných nasazeních měníte schéma existující databáze místo vytvoření nové databáze. Jak je popsáno v předchozí části, nemůžete do databázové role přidat uživatele, dokud nevytvoříte databázi z zjevné důvodů.

**Mapování přihlašovacích údajů účtu nasazení na roli databáze vlastníka\_databáze**

1. Otevřete SQL Server Management Studio jako dříve.
2. V okně **Průzkumník objektů** rozbalte uzel **zabezpečení** , rozbalte uzel **přihlášení** a potom poklikejte na přihlašovací jméno účtu počítače (například **FABRIKAM\matt**).
3. V dialogovém okně **Vlastnosti přihlášení** klikněte na **mapování uživatelů**.
4. V poli **Uživatelé namapované na tuto tabulku přihlášení** vyberte název vaší databáze (například **ContactManager**).
5. V seznamu **členství databázové role pro:** *[název databáze]* vyberte roli **vlastníka\_DB** .

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. Klikněte na tlačítko **OK**.

## <a name="conclusion"></a>Závěr

Váš databázový server by teď měl být připravený přijmout vzdálená nasazení databáze a umožní vzdáleným webovým serverům služby IIS přístup k vašim databázím. Než se pokusíte nasadit a používat databáze, možná budete chtít tyto klíčové body ověřit:

- Nakonfigurovali jste SQL Server, aby přijímala vzdálená připojení TCP/IP?
- Nakonfigurovali jste brány firewall, aby povolovaly SQL Server provoz?
- Vytvořili jste přihlášení k účtu počítače pro každý webový server, který bude mít přístup k SQL Server?
- Zahrnuje vaše nasazení databáze skript pro vytvoření mapování rolí uživatele nebo je budete muset po prvním nasazení databáze ručně vytvořit?
- Vytvořili jste přihlášení k účtu nasazení a Přidali jste ho do role serveru **dbcreator** ?

## <a name="further-reading"></a>Další čtení

Pokyny k nasazení databázových projektů najdete v tématu [nasazení databázových projektů](../web-deployment-in-the-enterprise/deploying-database-projects.md). Pokyny k vytváření členství v databázových rolích spuštěním skriptu po nasazení najdete v tématu [nasazení členství databázové role do testovacích prostředí](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md). Pokyny k tomu, jak vyhovět jedinečným problémům s nasazením, které představují databáze členství, najdete v tématu [nasazení databází členství v podnikových prostředích](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md).

> [!div class="step-by-step"]
> [Předchozí](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [Další](creating-a-server-farm-with-the-web-farm-framework.md)
