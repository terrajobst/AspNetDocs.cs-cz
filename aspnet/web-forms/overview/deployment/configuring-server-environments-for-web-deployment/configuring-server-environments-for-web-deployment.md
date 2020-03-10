---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: Konfigurace serverových prostředí pro nasazení webu | Microsoft Docs
author: jrjlee
description: V tomto kurzu se dozvíte, jak nastavit prostředí serveru pro podporu jednoho nebo automatizovaného nasazení webu a publikování v různých Scen...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 073161ce4faa3b7ba6749d7dfbaa5309eeca4f74
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634468"
---
# <a name="configuring-server-environments-for-web-deployment"></a>Konfigurace serverového prostředí pro nasazení webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> V tomto kurzu se dozvíte, jak nastavit serverové prostředí pro podporu jednoho kliknutí nebo automatizovaného nasazení webu a publikování v různých různých scénářích. V tomto kurzu se dozvíte, jak provést různé úkoly, jako je například konfigurace webového serveru pro podporu specifických přístupů k nasazení a nastavení serverové farmy WFF (Web Farm Framework), a to spolu s přehledy založenými na scénářích, které poskytují komplexní doprovodné materiály vyšší úrovně.
> 
> V tomto kurzu se používá scénář nasazení společnosti Fabrikam, Inc., který je popsaný v tématu [Přehled scénářů Enterprise Web Deployment: scénář](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) , který obsahuje příklady a síťovou infrastrukturu.
> 
> Pro účely nizozemského překladu těchto kurzů navštivte [http://www.lucamorelli.it](http://www.lucamorelli.it).

Tento kurz obsahuje tato témata:

- [Výběr správného přístupu k nasazení webu](choosing-the-right-approach-to-web-deployment.md)
- [Scénář: Konfigurace testovacího prostředí pro nasazení webu](scenario-configuring-a-test-environment-for-web-deployment.md)
- [Scénář: Konfigurace přípravného prostředí pro nasazení webu](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [Scénář: Konfigurace provozního prostředí pro nasazení webu](scenario-configuring-a-production-environment-for-web-deployment.md)
- [Konfigurace webového serveru pro publikování nasazeného webu (vzdálený agent)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [Konfigurace webového serveru pro publikování nasazeného webu (obslužná rutina nasazení webu)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [Konfigurace webového serveru pro publikování nasazeného webu (offline nasazení)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [Konfigurace databázového serveru pro publikování nasazeného webu](configuring-a-database-server-for-web-deploy-publishing.md)
- [Vytvoření serverové farmy na platformě Web Farm Framework](creating-a-server-farm-with-the-web-farm-framework.md)
- [Konfigurace vlastností nasazeného cílového prostředí](configuring-deployment-properties-for-a-target-environment.md)

V prvním tématu se [zvolením správného přístupu k nasazení webu](choosing-the-right-approach-to-web-deployment.md)popisuje hlavní přístupy, které můžete použít k publikování webových aplikací pomocí nástroje pro nasazení webu Internetová informační služba (IIS) (Nasazení webu) 2,0. Také identifikuje scénáře, které jsou namapovány na každý přístup. Z tohoto místa obsahuje každé téma scénáře základní přehled úloh, které potřebujete k dokončení, a určuje témata, která budete potřebovat, abyste mohli tyto úlohy dokončit.

Pokud používáte přístup k souboru rozděleného projektu, který je popsaný v tématu [Principy procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md) pro sestavení a nasazení vašeho řešení, v konečném tématu, které [konfiguruje vlastnosti nasazení pro cílové prostředí](configuring-deployment-properties-for-a-target-environment.md), popisuje, jak nakonfigurovat soubory projektu specifické pro prostředí pro nasazení do různých cílových prostředí.

## <a name="key-technologies"></a>Klíčové technologie

Tento kurz se zaměřuje na použití těchto produktů a technologií k podpoře nasazení webu:

- IIS 7.5
- Nasazení webu 2. x
- WFF 2. x
- Služba webové správy služby IIS (WMSvc)

Tento kurz se také dotýká použití Windows serveru 2008 R2, SQL Server 2008 R2, ASP.NET 4,0 a ASP.NET MVC 3.

## <a name="other-tutorials-in-this-series"></a>Další kurzy v této řadě

Tato část tvoří řadu pěti kurzů pro nasazení webu na podnikové úrovni. Toto jsou další kurzy v řadě:

- [Nasazení webových aplikací v podnikových scénářích](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Tento úvodní obsah poskytuje kontextové pozadí pro řadu kurzů. Popisuje scénář kurzu a ukazuje, jak se úlohy a návody popsané v rámci řady vešly do širšího procesu správy životního cyklu aplikací (ALM).
- [Nasazení webu v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Tento kurz obsahuje koncepční Úvod do souborů projektu Microsoft Build Engine (MSBuild), kanál publikování na webu, Nasazení webu a další související technologie. Vysvětluje, jak můžete tyto nástroje použít společně ke správě složitých procesů nasazení.
- [Konfigurace Team Foundation Server pro nasazení webu](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) V tomto kurzu se dozvíte, jak nakonfigurovat Team Foundation Server (TFS) pro podporu různých scénářů nasazení, včetně automatizovaného nasazení v rámci procesu kontinuální integrace (CI) a ruční aktivace nasazení konkrétních sestavení.
- [Pokročilé nasazení podnikového webu](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). V tomto kurzu se dozvíte, jak provádět různé pokročilejší úlohy nasazení, jako je přizpůsobení nasazení databáze pro více prostředí, vyloučení souborů a složek z nasazení a přepnutí webových aplikací do režimu offline během procesu nasazení. .

> [!div class="step-by-step"]
> [Next](choosing-the-right-approach-to-web-deployment.md)
