---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 'Scénář: Konfigurace přípravného prostředí pro nasazení webu | Microsoft Docs'
author: jrjlee
description: Toto téma popisuje Typický scénář nasazení webu pro pracovní prostředí a vysvětluje úkoly, které je potřeba provést, aby bylo možné nastavit podobnou obálku...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: eaa61ca850817f8dd98955b59e94be93389bf256
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637842"
---
# <a name="scenario-configuring-a-staging-environment-for-web-deployment"></a>Scénář: Konfigurace přípravného prostředí pro nasazení webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje Typický scénář nasazení webu pro přípravné prostředí a vysvětluje úkoly, které je potřeba provést, aby bylo možné nastavit podobné prostředí.

Spousta organizací používá pro náhled aktualizací webových aplikací nebo webů pracovní prostředí. To uživatelům v organizaci umožní prozkoumat a zkontrolovat nové funkce nebo obsah před tím, než bude lokalita "v provozu" nebo jinými slovy nasazena v produkčním prostředí. Pracovní prostředí je navrženo tak, aby bylo co nejpřesněji replikované provozní prostředí, aby se zajistila reálná verze Preview. Tento druh přípravného prostředí má obvykle tyto charakteristiky:

- Prostředí se skládá z více webových serverů s vyrovnáváním zatížení a jednoho nebo více databázových serverů, často s Clustering s podporou převzetí služeb při selhání a zrcadlením databáze.
- Aplikace mohou být nasazeny ručně vývojářským týmem nebo automaticky serverem sestavení týmu.
- Účty uživatelů nebo procesů, které nasazují aplikace, nemají pravděpodobně oprávnění správce na pracovních serverech.
- Změny aplikací se nasazují často, takže prostředí musí podporovat nasazení v jednom kroku nebo automatizované.

> [!NOTE]
> Horizontální navýšení kapacity nasazení databáze napříč více servery je nad rámec tohoto kurzu. Další informace o této oblasti najdete v dokumentaci [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).

Například v našem [scénáři kurzu](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)Team Foundation Server (TFS) spravuje řešení Contact Manager. Správce TFS, Rob Walters, vytvořil definici sestavení, která vývojářům umožňuje aktivovat nasazení do přípravného prostředí podle potřeby.

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

Všimněte si, že ve většině případů nebudete nutně chtít nasadit nejnovější sestavení do přípravného prostředí. Místo toho je mnohem více pravděpodobnější, že budete chtít nasadit konkrétní sestavení, které již prošlo ověřením a ověřením v testovacím prostředí.

## <a name="solution-overview"></a>Přehled řešení

V tomto scénáři můžete tyto fakta odvodit z analýzy požadavků na nasazení:

- Účet uživatele nebo procesu, který provádí nasazení, nebude mít na pracovních serverech oprávnění správce, takže pracovní webové servery musí podporovat nasazení bez oprávnění správce. V takovém případě budete muset nakonfigurovat pracovní webové servery tak, aby používaly obslužnou rutinu Nasazení webu místo vzdáleného agenta.
- Pracovní prostředí obsahuje několik webových serverů, ale je potřeba, aby podporovalo jedno kliknutí nebo automatizované nasazení, takže budete muset k vytvoření serverové farmy použít rozhraní Web Farm Framework (WFF). Pomocí tohoto přístupu můžete nasadit aplikaci na jeden webový server (primární server) a WFF bude replikovat nasazení na všech ostatních webových serverech v přípravném prostředí.
- Účet uživatele nebo procesu, který provádí nasazení, musí mít oprávnění k vytváření databází. V takovém případě budete muset přidat účet do role serveru **dbcreator** na databázovém serveru kromě Konfigurace databázového serveru pro podporu vzdáleného přístupu a nasazení.

Tato témata obsahují všechny informace, které potřebujete k dokončení těchto úloh:

- [Vytvořte serverovou farmu s architekturou web farmu](creating-a-server-farm-with-the-web-farm-framework.md). V tomto tématu se dozvíte, jak vytvořit a nakonfigurovat serverovou farmu pomocí WFF, takže se na více webových serverech s vyrovnáváním zatížení replikují aplikace a komponenty a součásti a webové platformy, nastavení konfigurace a weby a aplikace.
- [Konfigurace webového serveru pro publikování nasazení webu (obslužná rutina nasazení webu)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) Toto téma popisuje, jak vytvořit webový server, který podporuje publikování Nasazení webu, pomocí přístupu vzdáleného agenta počínaje čistým sestavením systému Windows Server 2008 R2.
- [Nakonfigurujte databázový server pro publikování nasazení webu](configuring-a-database-server-for-web-deploy-publishing.md). Toto téma popisuje, jak nakonfigurovat databázový server pro podporu vzdáleného přístupu a nasazení, počínaje od výchozí instalace SQL Server 2008 R2.

## <a name="further-reading"></a>Další čtení

Pokyny ke konfiguraci typického testovacího prostředí pro vývojáře naleznete v tématu [scénář: konfigurace testovacího prostředí pro nasazení webu](scenario-configuring-a-test-environment-for-web-deployment.md). Pokyny ke konfiguraci typického provozního prostředí najdete v tématu [scénář: Konfigurace provozního prostředí pro nasazení webu](scenario-configuring-a-production-environment-for-web-deployment.md).

> [!div class="step-by-step"]
> [Předchozí](scenario-configuring-a-test-environment-for-web-deployment.md)
> [Další](scenario-configuring-a-production-environment-for-web-deployment.md)
