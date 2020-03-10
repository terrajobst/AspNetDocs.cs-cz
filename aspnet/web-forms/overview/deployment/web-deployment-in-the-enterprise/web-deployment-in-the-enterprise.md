---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: Nasazení webu v podniku | Microsoft Docs
author: jrjlee
description: V tomto kurzu se dozvíte, jak vyhovět hodně problémům, se kterými se setkáte při správě nasazení webových aplikací na podnikové úrovni do devel...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: bc7bb676a71af4ec3451aa3adf3c03ce3b5200d5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628168"
---
# <a name="web-deployment-in-the-enterprise"></a>Nasazení webu v podniku

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> V tomto kurzu se dozvíte, jak vyhovět hodně problémům, se kterými se setkáte při správě nasazení webových aplikací na úrovni podniku ve vývojovém, testovacím, přípravném a produkčním prostředí. Tento kurz obsahuje referenční řešení společně s kombinací koncepčního a podrobného obsahu, který vás provede různými běžnými úkoly a postupy.
> 
> Pro účely nizozemského překladu těchto kurzů navštivte [http://www.lucamorelli.it](http://www.lucamorelli.it).

## <a name="enterprise-deployment-challenges"></a>Problémy s podnikovým nasazením

Organizace často narazí na tyto výzvy, když vypadají při správě nasazení komplexních podnikových řešení:

- Musíte být schopni nasadit projekty do více prostředí, jako jsou vývojové nebo testovací prostředí, pracovní platformy a provozní servery. Řešení musí být nasazené s jiným nastavením konfigurace pro každé prostředí.
- V rámci jednoho kroku nebo procesu automatického sestavení a nasazení je třeba nasadit více závislých projektů současně.
- Musíte být schopni nasazovat nasazení z automatizovaného procesu. Například chcete použít proces průběžné integrace (CI) k nasazení webových aplikací do testovacího prostředí, když je nový kód vrácen se změnami.
- Musíte být schopni řídit proces nasazení a nastavit proměnné pro nasazení mimo sadu Visual Studio, protože vývojáři pravděpodobně nemají správné nastavení konfigurace nebo potřebná pověření pro každé cílové prostředí.
- Je nutné nasadit databázové projekty založené na schématu a zachovat existující data v následných nasazeních.
- Databáze členství je nutné nasadit na základě ad hoc bez nutnosti nasazovat data uživatelského účtu. Je také možné, že budete muset aktualizovat schéma nasazených databází členství, aniž byste ztratili stávající data uživatelského účtu.
- Pokud nasazujete obsah do různých cílových prostředí, je potřeba vyloučit určité soubory nebo složky.

## <a name="overview-of-approach"></a>Přehled přístupu

V tomto kurzu spolu s dalšími kurzy v této sérii používá tento přístup na nejvyšší úrovni ke splnění výzev popsaných výše.

- **Použijte vlastní soubory projektu Microsoft Build Engine (MSBuild) k řízení celkového procesu sestavení a nasazení.**
- To umožňuje sestavovat a nasazovat každý projekt v řešení jako součást jediné operace umožňující skriptování.
- Nastavení specifická pro prostředí se konfigurují pomocí jednoduchých souborů projektu specifických pro konkrétní prostředí. Na rozdíl od přístupu k systému Visual Studio orientovaného k použití konfigurací řešení a publikování profilů ke konfiguraci nasazení pro různá prostředí vám tento přístup umožňuje nakonfigurovat a spravovat proces nasazení mimo sadu Visual Studio. To znamená, že vývojáři nebudou potřebovat předem znalosti připojovacích řetězců, koncových bodů služby, přihlašovacích údajů serveru a dalších proměnných nasazení pro cílová prostředí.
- Vlastní soubory projektu mohou být vyvolány týmem Build jako součást pracovního postupu Team Foundation Server (TFS). To vám umožní nakonfigurovat automatizované nasazení pro scénáře CI.

**K zabalení a nasazení projektů webové aplikace použijte nástroj pro nasazení webu Internetová informační služba (IIS) (Nasazení webu).**

- Nasazení webu poskytuje rozhraní, které umožňuje balení a nasazení obsahu webové aplikace na cílový webový server služby IIS, spolu se závislostmi, nastaveními konfigurace, nastavením zabezpečení a dalšími požadavky.
- Celý proces balení a nasazování můžete řídit v rámci vlastních souborů projektu MSBuild. Můžete také manipulovat s nastaveními konfigurace dodanými do balíčku pro nasazení webu, například připojovacími řetězci, koncovými body služby a podrobnostmi o cílové službě IIS.
- Nasazení webu společně s kanálem publikování na webu nabízí spoustu bodů rozšiřitelnosti, které umožňují přizpůsobit vaše nasazení. Můžete například snadno vyloučit nechtěné soubory a složky z balíčků pro nasazení webu.

**K nasazení a aktualizaci schémat databáze použijte nástroj VSDBCMD. exe.**

- VSDBCMD umožňuje nasadit databáze ze souboru schématu databáze (. dbschema), který je generován při sestavování projektu databáze aplikace Visual Studio. Naproti tomu funkce nasazení databáze zahrnutá v Nasazení webu je lépe vhodná pro nasazení stávajících databází z místní instance SQL Server.
- Na rozdíl od funkcí sady Visual Studio pro nasazení databázových projektů umožňuje VSDBCMD nasazovat rozdílové aktualizace stávající cílové databáze. Díky tomu můžete při upgradu schématu databáze zachovat veškerá stávající data.
- Příkazy VSDBCMD můžete spouštět v rámci vlastních souborů projektu MSBuild.

## <a name="content-map"></a>Mapa obsahu

Tento kurz obsahuje témata, která spadají do čtyř hlavních oblastí.

Tato témata představují referenční řešení&#x2014;v řešení&#x2014;správce kontaktů a popisují, jak ho stáhnout a nakonfigurovat na místním počítači:

- [Řešení správce kontaktů](the-contact-manager-solution.md)
- [Nastavení řešení správce kontaktů](setting-up-the-contact-manager-solution.md)

Tato témata představují soubory projektu nástroje MSBuild, popište, jak můžete vytvářet a používat vlastní soubory projektu, a projít si postup nasazení pro řešení Správce kontaktů:

- [Vysvětlení souboru projektu](understanding-the-project-file.md)
- [Vysvětlení procesu sestavení](understanding-the-build-process.md)

Tato témata popisují nasazení webové aplikace, včetně způsobu, jakým proces sestavení a vytváření balíčků funguje, jak se proces sestavení integruje s kanálem publikování na webu, jak upravit parametry nasazení a jak nasadit webové balíčky do cílového umístění. Environment

- [Sestavení a balení projektů webových aplikací](building-and-packaging-web-application-projects.md)
- [Konfigurace parametrů nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md)
- [Nasazení webových balíčků](deploying-web-packages.md)

- [Nasazení databázových projektů](deploying-database-projects.md) popisuje různé techniky, které můžete použít k nasazení databázových projektů sady Visual Studio, a to spolu s výhodami a nevýhodami každého přístupu. [Vytvoření a spuštění souboru příkazů pro nasazení](creating-and-running-a-deployment-command-file.md) popisuje, jak vytvořit jednoduchý soubor příkazů, který zapouzdřuje vaši logiku nasazení a umožňuje nasazení složitých řešení jako procesu s jedním krokem.
- Nakonec se po [ruční instalaci webových balíčků](manually-installing-web-packages.md) tento kurz dokončí tím, že se vám ukáže, jak importovat webové balíčky do služby IIS.

## <a name="key-technologies"></a>Klíčové technologie

Témata v tomto kurzu primárně využívají tyto technologie ke správě sestavení a nasazení:

- Visual Studio 2010
- MSBuild
- IIS 7.5
- Nasazení webu 2.0
- Nástroj pro nasazení databáze VSDBCMD. exe

## <a name="other-tutorials-in-this-series"></a>Další kurzy v této řadě

Tato část tvoří řadu pěti kurzů pro nasazení webu na podnikové úrovni. Toto jsou další kurzy v řadě:

- [Nasazení webových aplikací v podnikových scénářích](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Tento úvodní obsah poskytuje kontextové pozadí pro řadu kurzů. Popisuje scénář kurzu a ukazuje, jak se úlohy a návody popsané v rámci řady vešly do širšího procesu správy životního cyklu aplikací (ALM).
- [Konfigurují se serverová prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). V tomto kurzu se dozvíte, jak nakonfigurovat servery Windows pro podporu různých scénářů nasazení, včetně nasazení vzdáleného webového balíčku pomocí služby Web Deployment Agent Service (vzdálený Agent) nebo obslužné rutiny Nasazení webu a nasazení vzdálené databáze. Poskytuje pokyny k výběru vhodné metody nasazení pro vlastní prostředí a popisuje, jak používat webové serverové farmy (WFF) k replikaci nasazených webových aplikací napříč všemi webovými servery v serverové farmě.
- [Konfigurace Team Foundation Server pro nasazení webu](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) V tomto kurzu se dozvíte, jak nakonfigurovat TFS pro podporu různých scénářů nasazení, včetně automatizovaného nasazení v rámci procesu CI a ruční aktivace nasazení konkrétních sestavení.
- [Pokročilé nasazení podnikového webu](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). V tomto kurzu se dozvíte, jak provádět různé pokročilejší úlohy nasazení, jako je přizpůsobení nasazení databáze pro více prostředí, vyloučení souborů a složek z nasazení a přepnutí webových aplikací do režimu offline během procesu nasazení. .

> [!div class="step-by-step"]
> [Next](the-contact-manager-solution.md)
