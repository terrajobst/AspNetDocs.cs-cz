---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: 'Scénář: Konfigurace provozního prostředí pro nasazení webu | Microsoft Docs'
author: jrjlee
description: Toto téma popisuje Typický scénář nasazení webu pro produkční prostředí a vysvětluje úkoly, které je potřeba provést, aby bylo možné nastavit podobný postup...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2d76e715cdbf6ec484fa0ff98b3b3d1d8dfd3961
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635420"
---
# <a name="scenario-configuring-a-production-environment-for-web-deployment"></a>Scénář: Konfigurace provozního prostředí pro nasazení webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje Typický scénář nasazení webu pro produkční prostředí a vysvětluje úkoly, které je potřeba provést, aby bylo možné nastavit podobné prostředí.

Provozní prostředí je konečný cíl webové aplikace nebo webu. V tomto okamžiku byla aplikace přes testování nasazená do přípravného prostředí a je připravená na "jít živě". Charakteristiky produkčního prostředí se můžou výrazně lišit v závislosti na povaze a účelu vašeho webového obsahu, velikosti vaší organizace, cílové cílové skupině a mnoha dalších faktorech. Ve scénáři podnikového škálování můžou mít provozní prostředí tyto vlastnosti:

- Prostředí se skládá z více webových serverů s vyrovnáváním zatížení a jednoho nebo více databázových serverů, často s Clustering s podporou převzetí služeb při selhání a zrcadlením databáze.
- Pokud je prostředí orientované na Internet, bude pravděpodobně oddělené od vaší interní sítě. Může být v jiné podsíti v hraniční síti, může být v jiné doméně a může být na zcela jiné síťové infrastruktuře.
- Vývojáři a účty procesu sestavení serveru mají vysoce pravděpodobně oprávnění správce na provozních serverech.
- Změny aplikací se nasazují v méně častých intervalech než testovací nebo pracovní nasazení.

> [!NOTE]
> Horizontální navýšení kapacity nasazení databáze napříč více servery je nad rámec tohoto kurzu. Další informace o této oblasti najdete v dokumentaci [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).

Například v našem [scénáři](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)týmový server sestavení zahrnuje definice sestavení, které umožní uživatelům vytvářet řešení Správce kontaktů a nasazovat ho do přípravného prostředí v jednom kroku. Když je aplikace připravená k nasazení do produkčního prostředí, z důvodu omezení zavedených požadavky na zabezpečení a síťovou infrastrukturou musí správce produkčního prostředí ručně zkopírovat webový balíček na provozní webový server a importovat Správce prostřednictvím Internetová informační služba (IIS).

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a>Přehled řešení

V tomto scénáři můžete tyto fakta odvodit z analýzy požadavků na nasazení:

- Z důvodu omezení zabezpečení a konfigurace sítě nemůžete konfigurovat produkční prostředí pro podporu jednoho nebo automatizovaného nasazení. Jediným možným přístupem v tomto scénáři je nasazení v režimu offline.
- Provozní prostředí obsahuje více webových serverů, takže můžete k vytvoření serverové farmy použít rozhraní Web Farm Framework (WFF). Pomocí tohoto přístupu správce potřebuje aplikaci importovat jenom na jeden webový server (primární server) a WFF replikuje nasazení na všechny ostatní webové servery v produkčním prostředí.

Tato témata obsahují všechny informace, které potřebujete k dokončení těchto úloh:

- [Vytvořte serverovou farmu s architekturou web farmu](configuring-a-database-server-for-web-deploy-publishing.md). V tomto tématu se dozvíte, jak vytvořit a nakonfigurovat serverovou farmu pomocí WFF, takže se na více webových serverech s vyrovnáváním zatížení replikují aplikace a komponenty a součásti a webové platformy, nastavení konfigurace a weby a aplikace.
- [Konfigurace webového serveru pro publikování nasazení webu (offline nasazení)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md). Toto téma popisuje, jak vytvořit webový server, který umožňuje správcům importovat a nasazovat webové balíčky ručně, počínaje čistým sestavením systému Windows Server 2008 R2.
- [Nakonfigurujte databázový server pro publikování nasazení webu](configuring-a-database-server-for-web-deploy-publishing.md). Toto téma popisuje, jak nakonfigurovat databázový server pro podporu vzdáleného přístupu a nasazení, počínaje od výchozí instalace SQL Server 2008 R2.

## <a name="further-reading"></a>Další čtení

Pokyny ke konfiguraci typického testovacího prostředí pro vývojáře naleznete v tématu [scénář: konfigurace testovacího prostředí pro nasazení webu](scenario-configuring-a-test-environment-for-web-deployment.md). Pokyny ke konfiguraci typického přípravného prostředí najdete v tématu [scénář: Konfigurace přípravného prostředí pro nasazení webu](scenario-configuring-a-staging-environment-for-web-deployment.md).

> [!div class="step-by-step"]
> [Předchozí](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [Další](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
