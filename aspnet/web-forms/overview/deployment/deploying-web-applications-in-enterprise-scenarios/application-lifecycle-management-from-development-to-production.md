---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: 'Správa životního cyklu aplikací: od vývoje až po produkční prostředí | Microsoft Docs'
author: jrjlee
description: Toto téma ukazuje, jak fiktivní společnost spravuje nasazení webové aplikace ASP.NET prostřednictvím testovacích, testovacích a produkčních prostředí jako nominální hodnotu...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 230cf4393db0ee19cfc42ed54359d61e7926a49d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640663"
---
# <a name="application-lifecycle-management-from-development-to-production"></a>Správa životního cyklu aplikace: Od vývoje k ostrému provozu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma ukazuje, jak fiktivní společnost spravuje nasazení webové aplikace v ASP.NET prostřednictvím testovacích, pracovních a produkčních prostředí jako součást procesu průběžného vývoje. V celém tématu jsou odkazy k dispozici k dalším informacím a návodům k provádění konkrétních úkolů.
> 
> Téma je navrženo tak, aby poskytovalo přehled o [řadě kurzů](deploying-web-applications-in-enterprise-scenarios.md) při nasazení webu v podniku. Nedělejte si starosti, pokud neznáte některé z konceptů&#x2014;, které jsou zde popsané, v následujících kurzech získáte podrobné informace o všech těchto úlohách a technikách.
> 
> > [!NOTE]
> > V zájmu zjednodušení se v tomto tématu nezabývá aktualizace databází v rámci procesu nasazení. Provádění přírůstkových aktualizací pro databáze je ale požadavkem na mnoho scénářů podnikového nasazení a můžete najít pokyny, jak to provést později v této sérii kurzů. Další informace najdete v tématu [nasazení databázových projektů](../web-deployment-in-the-enterprise/deploying-database-projects.md).

## <a name="overview"></a>Přehled

Proces nasazení, který je znázorněný tady, je založený na scénáři nasazení společnosti Fabrikam, Inc., který je popsaný v tématu [Přehled podnikového nasazení webu: scénář](enterprise-web-deployment-scenario-overview.md) Před prozkoumáním tohoto tématu byste si měli přečíst přehled scénářů. V podstatě se scénář zabývá tím, jak organizace spravuje nasazení rozumně složité webové aplikace, [řešení Contact Manageru](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), a to prostřednictvím různých fází v typickém podnikovém prostředí.

V rámci vysoké úrovně řešení Správce kontaktů prochází těmito fázemi v rámci procesu vývoje a nasazení:

1. Vývojář zkontroluje kód v Team Foundation Server (TFS) 2010.
2. TFS sestaví kód a spustí všechny testy jednotek přidružené k týmovému projektu.
3. TFS nasadí řešení do testovacího prostředí.
4. Tým pro vývojáře ověří a ověří řešení v testovacím prostředí.
5. Správce přípravného prostředí provádí nasazení "Co když" do přípravného prostředí, aby bylo možné zjistit, zda nasazení způsobí nějaké problémy.
6. Správce přípravného prostředí provádí živé nasazení do přípravného prostředí.
7. Řešení přechází k testování přijetí uživateli v přípravném prostředí.
8. Balíčky pro nasazení webu se ručně naimportují do produkčního prostředí.

Tyto fáze tvoří část průběžného vývojového cyklu.

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

V praxi je proces od tohoto procesu poněkud složitější, protože uvidíte, kdy se podíváme na každou fázi podrobněji. Společnost Fabrikam, Inc. používá pro každé cílové prostředí jiný přístup k nasazení.

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

Zbývající část tohoto tématu prověřuje tyto klíčové fáze životního cyklu nasazení:

- **Požadavky**: jak budete potřebovat nakonfigurovat serverovou infrastrukturu před tím, než zadáte svou logiku nasazení.
- **Počáteční vývoj a nasazení**: co je potřeba udělat před prvním nasazením řešení.
- **Nasazení k testování**: Jak zabalit a nasadit obsah do testovacího prostředí automaticky, když vývojář kontroluje nový kód.
- **Nasazení do přípravy**: jak nasadit konkrétní sestavení do přípravného prostředí a jak provádět nasazení "Co kdyby", aby se zajistilo, že nasazení nebude způsobovat žádné problémy.
- **Nasazení do produkčního**prostředí: Jak importovat webové balíčky do provozního prostředí, když síťová infrastruktura brání vzdálenému nasazení.

## <a name="prerequisites"></a>Předpoklady

Prvním úkolem v jakémkoli scénáři nasazení je zajistit, aby serverová infrastruktura splňovala požadavky vašich nástrojů a technik nasazení. V tomto případě společnost Fabrikam, Inc. nakonfigurovala svoji serverovou infrastrukturu jako tuto:

- Sada TFS je nakonfigurována tak, aby zahrnovala kolekci týmového projektu, kontroléry sestavení a agenty sestavení. Další informace najdete v tématu [konfigurace Team Foundation Server pro automatizované nasazení webu](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) .
- Testovací prostředí je nakonfigurované tak, aby přijímalo vzdálená nasazení pomocí služby Web Deployment Agent ("vzdálený agent"), jak je popsáno v tématu [scénář: konfigurace testovacího prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md) a [Konfigurace webového serveru pro nasazení webu publikování (vzdálený Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).
- Pracovní prostředí je nakonfigurované tak, aby přijímalo vzdálená nasazení pomocí koncového bodu obslužné rutiny Nasazení webu, jak je popsáno v tématu [scénář: Konfigurace přípravného prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md) a [Konfigurace webového serveru pro Nasazení webu publikování (nasazení webu obslužné rutiny)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).
- Produkční prostředí je nakonfigurované tak, aby umožňovalo správci ručně importovat balíčky pro nasazení webu do služby Internetová informační služba (IIS), jak je popsáno v tématu [scénář: Konfigurace provozního prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md) a [Konfigurace webového serveru pro nasazení webu publikování (offline nasazení)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).

## <a name="initial-development-and-deployment"></a>Počáteční vývoj a nasazení

Předtím, než tým společnosti Fabrikam, Inc. může nasadit řešení Správce kontaktů poprvé, musí provádět tyto úlohy:

- Vytvořte nový týmový projekt v sadě TFS.
- Vytvořte soubory projektu Microsoft Build Engine (MSBuild), které obsahují logiku nasazení.
- Vytvořte definice sestavení TFS, které aktivují procesy nasazení.

### <a name="create-a-new-team-project"></a>Vytvořit nový týmový projekt

- Správce TFS, Rob Walters, vytvoří nový týmový projekt pro aplikaci, jak je popsáno v [tématu Vytvoření týmového projektu v TFS](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md). V dalším kroku vedoucí vývojář, matný Hink vytvoří kostru řešení. Zkontroluje své soubory do nového týmového projektu v TFS, jak je popsáno v tématu [Přidání obsahu do správy zdrojového kódu](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md).

### <a name="create-the-deployment-logic"></a>Vytvoření logiky nasazení

Mat Hink vytváří různé vlastní soubory projektu MSBuild pomocí přístupu k rozdělenému souboru projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md). Matný vytvoří:

- Soubor projektu s názvem *Publish. proj* , který spouští proces nasazení. Tento soubor obsahuje cíle MSBuild, které sestavují projekty v řešení, vytváří webové balíčky a nasazují balíčky do prostředí cílového serveru.
- Soubory projektu specifické pro prostředí s názvem *ENV-dev. proj* a *ENV-Stage. proj*. Obsahují nastavení, která jsou specifická pro testovací prostředí a pracovní prostředí, jako jsou připojovací řetězce, koncové body služby a podrobnosti vzdálené služby, které obdrží webový balíček. Pokyny k výběru správného nastavení pro konkrétní cílová prostředí najdete v tématu [Konfigurace vlastností nasazení pro cílové prostředí](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

Pro spuštění nasazení spustí uživatel soubor *Publish. proj* pomocí nástroje MSBuild nebo týmu Build a určí umístění relevantního souboru projektu specifického pro prostředí (*ENV-dev. proj* nebo *ENV-Stage. proj*) jako argument příkazového řádku. Soubor *Publish. proj* pak importuje soubor projektu specifický pro prostředí a vytvoří kompletní sadu pokynů pro publikování pro každé cílové prostředí.

> [!NOTE]
> Způsob fungování těchto vlastních souborů projektu je nezávislý na mechanismu, který používáte k vyvolání nástroje MSBuild. Například můžete použít příkazový řádek MSBuild přímo, jak je popsáno v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md). Můžete spustit soubory projektu z příkazového souboru, jak je popsáno v tématu [Vytvoření a spuštění souboru příkazů nasazení](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md). Alternativně můžete spustit soubory projektu z definice sestavení v TFS, jak je popsáno v [tématu Vytvoření definice sestavení, která podporuje nasazení](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).  
> V každém případě je konečný výsledek stejný&#x2014;nástroj MSBuild spustí sloučený soubor projektu a nasadí vaše řešení do cílového prostředí. To vám poskytne značnou flexibilitu při aktivaci procesu publikování.

Po vytvoření vlastních souborů projektu přidá tento podklad do složky řešení a zkontroluje je do správy zdrojového kódu.

### <a name="create-build-definitions"></a>Vytvořit definice sestavení

Jako poslední přípravný úkol, matný a Rob spolupracuje a vytvoří tři definice sestavení pro nový týmový projekt:

- **DeployToTest**. Tím se vytvoří řešení Správce kontaktů a nasadí se do testovacího prostředí pokaždé, když dojde k vrácení se změnami.
- **DeployToStaging**. Tím dojde k nasazení prostředků z určeného předchozího sestavení do přípravného prostředí, když vývojář zařadí do fronty sestavení.
- **DeployToStaging-whatIf**. V případě, že vývojář zařadí do fronty sestavení, provede nasazení do pracovního prostředí.

Níže uvedené části poskytují další podrobnosti o každé z těchto definicí sestavení.

## <a name="deployment-to-test"></a>Nasazení k testování

Vývojový tým ve společnosti Fabrikam, Inc. udržuje testovací prostředí pro provádění nejrůznějších softwarových testovacích aktivit, jako je ověřování a ověřování, testování použitelnosti, testování kompatibility a ad hoc nebo průzkumné testování.

Vývojový tým vytvořil v TFS definici sestavení s názvem **DeployToTest**. Tato definice sestavení používá Trigger průběžné integrace, což znamená, že se proces sestavení spouští pokaždé, když člen týmu Fabrikam, Inc. vývojový tým provede vrácení se změnami. Při aktivaci sestavení bude definice sestavení:

- Sestavte řešení ContactManager. sln. To zase sestaví každý projekt v rámci řešení.
- Spusťte všechny testy jednotek ve struktuře složek řešení (Pokud se řešení úspěšně sestaví).
- Spusťte vlastní soubory projektu, které řídí proces nasazení (Pokud se řešení úspěšně sestaví a projde všemi testy jednotek).

Konečným výsledkem je, že pokud se řešení úspěšně sestaví a předá testy jednotek, jsou webové balíčky a další prostředky nasazení nasazeny do testovacího prostředí.

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>Jak proces nasazení funguje?

Definice sestavení **DeployToTest** poskytuje tyto argumenty pro MSBuild:

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]

Vlastnosti balíčku **DeployOnBuild = true** a **DeployTarget =** jsou použity v případě, že sestavení týmu sestaví projekty v rámci řešení. Pokud se jedná o projekt webové aplikace, tyto vlastnosti instruují nástroj MSBuild, aby vytvořil balíček pro nasazení webu pro projekt. Vlastnost **TargetEnvPropsFile** instruuje soubor *Publish. proj* , kde lze najít soubor projektu specifický pro prostředí k importu.

> [!NOTE]
> Podrobný návod, jak vytvořit definici sestavení, naleznete v tématu [Vytvoření definice sestavení, která podporuje nasazení](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).

Soubor *Publish. proj* obsahuje cíle, které sestavují jednotlivé projekty v řešení. Nicméně obsahuje také podmíněnou logiku, která přeskočí tyto cíle sestavení, pokud spouštíte soubor v týmovém sestavení. Díky tomu můžete využít výhod dalších funkcí sestavení, které týmové sestavení nabízí, jako je možnost spustit testy jednotek. Pokud sestavení řešení nebo testování částí selže, soubor *Publish. proj* nebude proveden a aplikace nebude nasazena.

Podmíněná logika je dosažena vyhodnocením vlastnosti **BuildingInTeamBuild** . Toto je vlastnost MSBuild, která je automaticky nastavena na **hodnotu true** při vytváření projektů pomocí týmového sestavení.

## <a name="deployment-to-staging"></a>Nasazení do přípravy

Pokud sestavení splňuje všechny požadavky vývojářského týmu v testovacím prostředí, tým může chtít nasadit stejné sestavení do přípravného prostředí. Přípravná prostředí jsou obvykle nakonfigurovaná tak, aby odpovídala charakteristikám produkčního a "živého" prostředí, například z hlediska specifikací serveru, operačních systémů a softwaru a konfigurace sítě. Přípravná prostředí se často používají pro zátěžové testování, testování přijetí uživatelů a širší interní recenze. Sestavení jsou nasazena do přípravného prostředí přímo ze serveru sestavení.

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

Definice sestavení použité k nasazení řešení do přípravného prostředí, **DeployToStaging-whatIf** a **DeployToStaging**, sdílejí tyto charakteristiky:

- Nevytvářejí ve skutečnosti nic. Když Rob nasadí řešení do přípravného prostředí, chce nasadit konkrétní existující sestavení, které je již ověřeno a ověřeno v testovacím prostředí. Definice sestavení pouze potřebují spustit vlastní soubory projektu, které řídí proces nasazení.
- Když Rob spustí sestavení, použije parametry sestavení k určení, které sestavení obsahuje prostředky, které chce nasadit ze serveru sestavení.
- Definice sestavení nejsou automaticky spouštěny. Rob ručně zařadí do fronty sestavení, když chce nasadit řešení do přípravného prostředí.

Toto je proces vysoké úrovně pro nasazení do přípravného prostředí:

1. Správce přípravného prostředí, Rob Walters, zařadí sestavení pomocí definice sestavení **DeployToStaging-whatIf** . Rob používá parametry definice sestavení k určení, které sestavení chce nasadit.
2. Definice sestavení **DeployToStaging-whatIf** spustí vlastní soubory projektu v režimu "co if". Tato operace generuje soubory protokolu, jako by Rob prováděl živé nasazení, ale ve skutečnosti neprovede žádné změny v cílovém prostředí.
3. Rob zkontroluje soubory protokolu, aby zjistila důsledky nasazení v přípravném prostředí. Zejména Rob chce ověřit, co bude přidáno, co bude aktualizováno a co se odstraní.
4. Pokud je splněna Rob, že nasazení neprovede žádné nežádoucí změny stávajících prostředků nebo dat, zařadí sestavení do fronty pomocí definice sestavení **DeployToStaging** .
5. Definice sestavení **DeployToStaging** spustí vlastní soubory projektu. Ty publikují prostředky nasazení na primární webový server v přípravném prostředí.
6. Kontroler WFF (Web Farm Framework) synchronizuje webové servery v přípravném prostředí. Tím se aplikace zpřístupní na všech webových serverech v serverové farmě.

### <a name="how-does-the-deployment-process-work"></a>Jak proces nasazení funguje?

Definice sestavení **DeployToStaging** poskytuje tyto argumenty pro MSBuild:

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]

Vlastnost **TargetEnvPropsFile** instruuje soubor *Publish. proj* , kde lze najít soubor projektu specifický pro prostředí k importu. Vlastnost **OutputRoot** Přepisuje předdefinovanou hodnotu a označuje umístění složky sestavení, která obsahuje prostředky, které chcete nasadit. Když Rob zařadí do fronty sestavení, použije kartu **Parameters** k zadání aktualizované hodnoty vlastnosti **OutputRoot** .

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> Další informace o tom, jak vytvořit definici sestavení, naleznete v tématu [nasazení konkrétního sestavení](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md).

Definice sestavení **DeployToStaging-whatIf** obsahuje stejnou logiku nasazení jako definice sestavení **DeployToStaging** . Obsahuje ale dodatečný argument **whatIf = true**:

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]

V rámci souboru *Publish. proj* vlastnost **whatIf** označuje, že všechny prostředky nasazení by měly být publikovány v režimu "co if". Jinými slovy, soubory protokolu se generují, jako kdyby nasazení prošlo předem, ale v cílovém prostředí se nic nezměnilo. To vám umožní vyhodnotit dopad navrženého nasazení&#x2014;konkrétně, co se přidá, co se bude aktualizovat a co se odstraní&#x2014;, než budete ve skutečnosti dělat změny.

> [!NOTE]
> Další informace o tom, jak nakonfigurovat nasazení "Co je potřeba", najdete v tématu [provádění nasazení "What If"](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md).

Po nasazení aplikace na primární webový server v přípravném prostředí bude WFF automaticky synchronizovat aplikaci napříč všemi servery v serverové farmě.

> [!NOTE]
> Další informace o konfiguraci WFF pro synchronizaci webových serverů najdete v tématu [Vytvoření serverové farmy s rozhraním web Farm Framework](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md).

## <a name="deployment-to-production"></a>Nasazení do produkčního prostředí

Když je sestavení schváleno v přípravném prostředí, může tým společnosti Fabrikam, Inc. publikovat aplikaci do provozního prostředí. Provozní prostředí je místo, kde aplikace přechází "Live" a dostane cílovou cílovou skupinu koncových uživatelů.

Produkční prostředí je v internetové hraniční síti. To je izolované od interní sítě, která obsahuje server sestavení. Správce produkčního prostředí, Lisa Andrews, musí ručně zkopírovat balíčky pro nasazení webu ze serveru sestavení a importovat je do služby IIS na primárním provozním webovém serveru.

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

Toto je proces vysoké úrovně pro nasazení do produkčního prostředí:

1. Vývojářský tým doporučuje Lisa, že je sestavení připravené k nasazení do produkčního prostředí. Tým doporučuje Lisa umístění balíčků pro nasazení webu v ukládací složce na serveru sestavení.
2. Lisa shromažďuje webové balíčky ze serveru sestavení a kopíruje je do primárního webového serveru v provozním prostředí.
3. Lisa používá správce služby IIS k importu a publikování webových balíčků na primárním webovém serveru.
4. Kontroler WFF synchronizuje webové servery v produkčním prostředí. Tím se aplikace zpřístupní na všech webových serverech v serverové farmě.

### <a name="how-does-the-deployment-process-work"></a>Jak proces nasazení funguje?

Správce služby IIS obsahuje Průvodce importem balíčku aplikace, který usnadňuje publikování webových balíčků na webu služby IIS. Návod k provedení tohoto postupu najdete v tématu [Ruční instalace webových balíčků](../web-deployment-in-the-enterprise/manually-installing-web-packages.md).

## <a name="conclusion"></a>Závěr

Toto téma poskytuje ilustraci životního cyklu nasazení pro typickou webovou aplikaci na podnikové úrovni.

Toto téma tvoří část série kurzů, které poskytují pokyny k různým aspektům nasazení webové aplikace. V praxi existuje spousta dalších úkolů a důležitých informací v každé fázi procesu nasazení a není možné je pokrýt v jednom návodu. Další informace najdete v těchto kurzech:

- [Nasazení webu v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). V tomto kurzu se seznámíte se základními postupy pro nasazení webu pomocí nástrojů MSBuild a nástroje pro nasazení webu služby IIS (Nasazení webu).
- [Konfigurují se serverová prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). V tomto kurzu najdete pokyny ke konfiguraci prostředí Windows serveru pro podporu různých scénářů nasazení.
- [Konfigurace Team Foundation Server pro automatizované nasazení webu](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). V tomto kurzu najdete pokyny k integraci logiky nasazení do procesů sestavení TFS.
- [Pokročilé nasazení podnikového webu](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). V tomto kurzu najdete pokyny k tomu, jak vyhovět některým složitějším problémům s nasazením, které organizace čelí.

> [!div class="step-by-step"]
> [Předchozí](enterprise-web-deployment-scenario-overview.md)
