---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: 'Scénář: konfigurace testovacího prostředí pro nasazení webu | Microsoft Docs'
author: jrjlee
description: Toto téma popisuje Typický scénář nasazení webu pro vývojová a testovací prostředí a vysvětluje úkoly, které je potřeba provést, aby bylo možné nastavit si...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: d580e550f2461837f0e8a4e477273348b49cb53e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637814"
---
# <a name="scenario-configuring-a-test-environment-for-web-deployment"></a>Scénář: Konfigurace testovacího prostředí pro nasazení webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje Typický scénář nasazení webu pro vývojová a testovací prostředí a vysvětluje úkoly, které je potřeba provést, aby bylo možné nastavit podobné prostředí.

Když vývojáři pracují na webových aplikacích, často mají přístup k prostředí serveru, které můžou použít k testování změn ve svých aplikacích ve realistickém nastavení. Tento druh vývojového nebo testovacího prostředí má obvykle tyto charakteristiky:

- Prostředí se skládá z jednoho webového serveru a jednoho databázového serveru.
- Vývojáři mají obvykle na serverech oprávnění správce, aby je mohli nakonfigurovat tak, aby se prostředí nakonfigurovali na požadavky svých aplikací.
- Změny aplikací se nasazují často, takže prostředí musí podporovat nasazení v jednom kroku nebo automatizované.

Například v našem [scénáři](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)je matný Hink vývojářem ve společnosti Fabrikam, Inc. matný na řešení Správce kontaktů a pravidelně potřebuje nasazovat změny do testovacího prostředí. Matné je správce testovacího webového serveru a testovacího serveru databáze. Nejprve musí být matný schopný nasadit řešení přímo do testovacího prostředí.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

Jak pracovní postup a další vývojáři se připojují k týmu, řešení Správce kontaktů je nakonfigurované pro kontinuální integraci (CI) v Team Foundation Server (TFS). Kdykoli vývojář provede kontrolu obsahu, sestavení týmu by mělo vytvořit řešení, spustit všechny testy jednotek a automaticky nasadit řešení do testovacího prostředí.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a>Přehled řešení

Testovací prostředí musí podporovat jedno nebo automatizované nasazení ze vzdáleného počítače, takže máte možnost volit ze dvou hlavních přístupů. Můžete:

- Nakonfigurujte testovací webový server tak, aby podporoval nasazení pomocí webové Deployment Agent služby ("vzdálený agent").
- Nakonfigurujte testovací webový server tak, aby podporoval nasazení pomocí obslužné rutiny Nasazení webu.

> [!NOTE]
> Můžete také použít [nasazení webu na vyžádání](https://technet.microsoft.com/library/ee517345(WS.10).aspx) ("dočasný agent"). To se podobá přístupu ke vzdálenému agentům z pohledu požadavků a omezení.

V takovém případě mají vývojáři na cílových serverech oprávnění správce a testovací prostředí nepodléhá přísným omezením zabezpečení, takže logická volba je nakonfigurovat testovací webový server tak, aby podporoval nasazení pomocí vzdáleného agenta. To je méně složité a vyžaduje méně počáteční konfiguraci než přístup k obslužné rutině Nasazení webu. Také budete muset nakonfigurovat databázový server tak, aby podporoval vzdálený přístup a nasazení.

Tato témata obsahují všechny informace, které potřebujete k dokončení těchto úloh:

- [Nakonfigurujte webový server pro publikování nasazení webu (vzdálený Agent)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md). Toto téma popisuje, jak vytvořit webový server, který podporuje publikování Nasazení webu, pomocí přístupu vzdáleného agenta počínaje čistým sestavením systému Windows Server 2008 R2.
- [Nakonfigurujte databázový server pro publikování nasazení webu](configuring-a-database-server-for-web-deploy-publishing.md). Toto téma popisuje, jak nakonfigurovat databázový server pro podporu vzdáleného přístupu a nasazení, počínaje od výchozí instalace SQL Server 2008 R2.

## <a name="further-reading"></a>Další čtení

Pokyny ke konfiguraci typického přípravného prostředí najdete v tématu [scénář: Konfigurace přípravného prostředí pro nasazení webu](scenario-configuring-a-staging-environment-for-web-deployment.md). Pokyny ke konfiguraci typického provozního prostředí najdete v tématu [scénář: Konfigurace provozního prostředí pro nasazení webu](scenario-configuring-a-production-environment-for-web-deployment.md).

> [!div class="step-by-step"]
> [Předchozí](choosing-the-right-approach-to-web-deployment.md)
> [Další](scenario-configuring-a-staging-environment-for-web-deployment.md)
