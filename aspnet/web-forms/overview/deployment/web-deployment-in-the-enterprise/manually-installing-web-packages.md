---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: Ruční instalace webových balíčků | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak ručně importovat balíček pro nasazení webu do Internetová informační služba (IIS). Téma vytváření a balení webového Applicati...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: f778549d3e26989a2e71ef21171adec521842729
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634202"
---
# <a name="manually-installing-web-packages"></a>Ruční instalace webových balíčků

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak ručně importovat balíček pro nasazení webu do Internetová informační služba (IIS).
> 
> Téma [vytváření a balení projektů webových aplikací](building-and-packaging-web-application-projects.md) , které popisuje, jak Nástroj pro nasazení webu služby IIS (nasazení webu), ve spojení s Microsoft Build Engine (MSBuild) a kanálem publikování na webu (WPP), umožňuje zabalit vaše projekty webové aplikace do jednoho souboru ZIP. Tento soubor, který se běžně označuje jako balíček pro nasazení webu (nebo jednoduše balíček pro nasazení), obsahuje všechny informace o obsahu a konfiguraci, které služba IIS potřebuje k tomu, aby se vaše webová aplikace znovu vytvořila na webovém serveru.
> 
> Po vytvoření balíčku pro nasazení webu ho můžete publikovat na server IIS různými způsoby. V mnoha scénářích budete chtít využít výhod integračních bodů mezi MSBuild, WPP a Nasazení webu a vzdáleně vytvářet a instalovat webové balíčky v rámci automatizovaného nebo procesu sestavení a nasazení v jednom kroku. Tento postup je popsaný v tématu [nasazení webových balíčků](deploying-web-packages.md). To však není vždy možné. Předpokládejme, že chcete nasadit webovou aplikaci do produkčního prostředí s přístupem k Internetu. Z bezpečnostních důvodů je takové produkční prostředí přinejmenším pravděpodobně za bránou firewall v podsíti, která je oddělená od serveru sestavení, v hraniční síti (známé také jako DMZ, demilitarizovaná Zone a monitorovaná podsíť). V mnoha případech bude provozní prostředí v samostatné doméně nebo v fyzicky izolované síti.
> 
> V těchto scénářích může být jediným z možností, jak přenést webový balíček do cílového serveru a ručně ho importovat do služby IIS. I když tento přístup vylučuje automatizované nasazení, je stále vysoce efektivní technikou pro publikování webové aplikace&#x2014;, která jednoduše kopíruje jeden soubor zip na váš webový server a pomocí Průvodce vás provede procesem importu.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

## <a name="task-overview"></a>Přehled úlohy

K importu balíčku pro nasazení webu do služby IIS budete muset provést tyto úlohy vysoké úrovně:

- Vytvořte balíček pro nasazení webu pomocí příkazového řádku MSBuild, týmového sestavení nebo sady Visual Studio 2010.
- Kopírovat webový balíček na cílový webový server.
- Pomocí Průvodce importem balíčku aplikace ve Správci služby IIS nainstalujte webový balíček a zadejte hodnoty proměnných, jako jsou připojovací řetězce a koncové body služby.

V tomto tématu se dozvíte, jak provádět tyto postupy. V úlohách a návodech v tomto tématu se předpokládá, že už jste obeznámeni s koncepty za webovými balíčky, Nasazení webu a WPP. Další informace naleznete v tématu [sestavování a balení projektů webových aplikací](building-and-packaging-web-application-projects.md).

> [!NOTE]
> Toto téma se nejlépe používá ve spojení s [konfigurací webového serveru pro nasazení webu publikování (offline nasazení)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), které vysvětluje, jak nainstalovat požadované komponenty a připravit web IIS na Import balíčku.

## <a name="create-a-web-deployment-package"></a>Vytvoření balíčku pro nasazení webu

Prvním úkolem je vytvořit balíček pro nasazení webu pro projekt webové aplikace, který chcete nasadit. Webové balíčky můžete vytvořit různými způsoby.

**Přístup 1: Vytvořte balíček jako součást procesu sestavení se sadou Visual Studio**

Projekt webové aplikace můžete nakonfigurovat tak, aby po každém sestavení vytvořil balíček pro nasazení webu prostřednictvím karty **balíček/publikovat web** na stránkách vlastností projektu. Tento proces je popsán v tématu [sestavování a balení projektů webových aplikací](building-and-packaging-web-application-projects.md).

**Přístup 2: vytvoření balíčku jako součásti procesu sestavení pomocí nástroje MSBuild**

Pokud sestavíte projekt webové aplikace pomocí nástroje MSBuild přímo, a to buď pomocí vlastního souboru projektu MSBuild, nebo z příkazového řádku, můžete vytvořit balíček pro nasazení webu jako součást procesu sestavení zahrnutím vlastností **DeployOnBuild = true** a **DeployTarget = Package** do příkazu. Tento proces je popsán v tématu [Principy procesu sestavení](understanding-the-build-process.md).

**Přístup 3: vytvoření balíčku na vyžádání v aplikaci Visual Studio**

Balíček pro nasazení webu můžete v projektu webové aplikace kdykoli vytvořit v aplikaci Visual Studio 2010. Chcete-li to provést, klikněte v okně **Průzkumník řešení** pravým tlačítkem myši na projekt webové aplikace a poté klikněte na příkaz **sestavit balíček pro nasazení**.

![](manually-installing-web-packages/_static/image1.png)

**Přístup 4: vytvoření balíčku na vyžádání z příkazového řádku**

Balíček pro nasazení webu můžete vytvořit z příkazového řádku vyvoláním cíle **balíčku** na projekt webové aplikace pomocí nástroje MSBuild. Příkaz by měl vypadat takto:

[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]

Bez ohledu na to, jakou metodu použijete, je konečný výsledek stejný. WPP vytvoří balíček pro nasazení webu jako soubor zip spolu s různými podpůrnými prostředky ve výstupní složce pro váš projekt webové aplikace.

![](manually-installing-web-packages/_static/image2.png)

Pokud plánujete importovat webový balíček ručně, budete potřebovat pouze soubor zip. Zkopírujte tento soubor na cílový webový server a můžete zahájit proces importu.

## <a name="import-a-web-package-into-iis"></a>Import webového balíčku do služby IIS

Následující postup můžete použít k importu balíčku pro nasazení webu z místního systému souborů na web služby IIS. Před provedením tohoto postupu se ujistěte, že máte následující:

- Balíček pro nasazení webu byl zkopírován na webový server.
- Byl nakonfigurován webový server služby IIS pro hostování aplikace.

Další informace o konfiguraci webového serveru služby IIS pro podporu balíčků nasazení webu najdete v tématu [Konfigurace webového serveru pro nasazení webu publikování (offline nasazení)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).

**Import balíčku pro nasazení webu pomocí Správce služby IIS**

1. Ve Správci služby IIS klikněte v podokně **připojení** pravým tlačítkem na web IIS, přejděte na **nasadit**a pak klikněte na **importovat aplikaci**.

    ![](manually-installing-web-packages/_static/image3.png)
2. V Průvodci importem balíčku aplikace na stránce **Vybrat balíček** vyhledejte umístění balíčku pro nasazení webu a potom klikněte na **Další**.
3. Na stránce **Výběr obsahu balíčku** vymažte veškerý obsah, který nepotřebujete, a potom klikněte na tlačítko **Další**.

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > V mnoha případech možná nebudete chtít importovat vše, co je součástí balíčku pro nasazení webu. Například nebudete chtít, aby Nasazení webu mohl nahradit přidruženou databázi.  
    > Položky **udělit oprávnění** nastavte oprávnění pro cílový systém souborů, aby bylo zajištěno, že identita fondu aplikací bude mít přístup k fyzické složce, ve které je uložen obsah webu. Kromě toho je uživateli anonymního ověřování uděleno oprávnění ke čtení složky, aby mohla aplikace sloužit jako soubory typu MIME (Multipurpose Internet Mail Extensions). Pokud budete chtít, můžete tyto položky odebrat a nakonfigurovat oprávnění ručně.
4. Na stránce **zadat informace o balíčku aplikace** zadejte požadované informace.

    ![](manually-installing-web-packages/_static/image5.png)
5. Při vytváření webového balíčku služba WPP analyzuje konfigurační soubor pro vaši aplikaci a detekuje jakékoli proměnné, jako jsou připojovací řetězce a koncové body služby. V tomto případě:

    1. **Cesta aplikace** je cesta služby IIS, kam chcete nainstalovat aplikaci. Toto nastavení je společné pro všechny balíčky pro nasazení, které vytvoří WPP.
    2. **Adresa koncového bodu služby ContactService** je adresa, kterou by měla aplikace používat ke komunikaci s nasazenou službou WCF. Toto nastavení odpovídá záznamu v souboru *Web. config* .
    3. Nastavení prvního **připojovacího řetězce** je připojovací řetězec, který nasazení webu použít k nasazení databáze přidružené k aplikaci (v tomto případě databáze členství v ASP.NET). Toto nastavení odpovídá nastavení na kartě **Balení/publikování SQL** v aplikaci Visual Studio.
    4. Druhým **připojovacím řetězcem** je připojovací řetězec, který bude vaše aplikace ve skutečnosti používat ke komunikaci s databází, když je spuštěná a spuštěná. To odpovídá záznamu připojovacího řetězce v souboru *Web. config* .

        > [!NOTE]
        > Další informace o tom, odkud tyto parametry pocházejí, najdete v tématu [Konfigurace parametrů pro nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md).
6. Klikněte na **Další**.
7. Pokud se nejedná o první nasazení aplikace na tento web, budete vyzváni, abyste určili, zda chcete odstranit veškerý existující obsah před instalací. Zvolte možnost, která je vhodná pro vaše požadavky, a potom klikněte na tlačítko **Další**.

    ![](manually-installing-web-packages/_static/image6.png)
8. Až služba IIS dokončí instalaci balíčku, klikněte na **Dokončit**.

    ![](manually-installing-web-packages/_static/image7.png)

V tomto okamžiku jste úspěšně publikovali webovou aplikaci do služby IIS.

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak importovat balíček pro nasazení webu na web IIS pomocí Správce služby IIS. Tento přístup k publikování webové aplikace je vhodný v případě, že omezení zabezpečení nebo infrastruktury znemožňuje vzdálené nasazení nebo je nežádoucí.

## <a name="further-reading"></a>Další čtení

Pokyny ke konfiguraci webového serveru služby IIS pro podporu ručního importu webového balíčku najdete v tématu [Konfigurace webového serveru pro nasazení webu publikování (offline nasazení)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md). Obecnější pokyny k nasazení webových balíčků naleznete v tématu [Návod: nasazení projektu webové aplikace pomocí balíčku pro nasazení webu (část 1 ze 4)](https://msdn.microsoft.com/library/dd483479.aspx).

> [!div class="step-by-step"]
> [Předchozí](creating-and-running-a-deployment-command-file.md)
