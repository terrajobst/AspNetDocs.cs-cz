---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: Nasazení webových aplikací v podnikových scénářích pomocí sady Visual Studio 2010 | Microsoft Docs
author: jrjlee
description: Tato sada kurzů popisuje nástroje a techniky, které můžete použít k nasazení webových aplikací v různých podnikových scénářích. Vysvětluje, jak dosáhnout nejlepšího použití...
ms.author: riande
ms.date: 05/03/2012
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: eb7b82d16079d4d086af1919d092fb28db60d8b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574156"
---
# <a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a>Scénáře nasazení webových aplikací v podniku pomocí sady Visual Studio 2010

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Tato sada kurzů popisuje nástroje a techniky, které můžete použít k nasazení webových aplikací v různých podnikových scénářích. Vysvětluje, jak se dá nejlépe využít technologie, jako je Visual Studio 2010, Microsoft Build Engine (MSBuild), Internetová informační služba (IIS) 7,5, nástroj pro nasazení webu IIS (Nasazení webu), WFF (Web Farm Framework) a nástroje, jako je VSDBCMD. exe, do Zjednodušte a spravujte proces nasazení. Obsahuje koncepční přehledy a pokyny orientované na úlohy, které vám pomůžou:
> 
> - Zkontrolujte a navažte požadavky na nasazení pro webovou aplikaci na podnikové úrovni.
> - Nakonfigurujte testovací, pracovní a provozní prostředí webového serveru pro podporu nasazení webu.
> - Nakonfigurujte procesy průběžné integrace (CI) Team Foundation Server (TFS) pro podporu automatizovaného nasazení webu.
> - Nasaďte webové aplikace na podnikové úrovni do různých serverových prostředí s různými požadavky a omezeními.
> - Nasaďte změny webových aplikací, které běží v různých serverových prostředích.
> 
> > [!NOTE]
> > I když tyto kurzy popisují použití TFS jako serveru CI, doprovodné materiály jsou snadno přizpůsobené jakémukoli serveru CI. Pro pochopení a využití výukových kurzů nepotřebujete žádné podrobné znalosti TFS.
> 
> 
> Pro účely nizozemského překladu těchto kurzů navštivte [http://www.lucamorelli.it](http://www.lucamorelli.it).

## <a name="about-the-authors"></a>O autorech

Jason Novák je hlavní technik s [hlavním obsahem](http://www.contentmaster.com/) , kde spolupracuje s produkty a technologiemi Microsoftu, zejména se službami SharePoint a ASP.NET, po dobu několika let. Jason obsahuje PhD v computingu a je v současnosti MCPD a MCTS certifikováno. Technický blog k Jason si můžete přečíst na adrese [www.jrjlee.com](http://www.jrjlee.com/).

Benjamin Curry je hlavní technik s [hlavním obsahem](http://www.contentmaster.com/) , který má písemně psané dokumenty White Paper, dokumentaci k sadě SDK, prezentace v PowerPointu a školicí a Online školicí kurzy, a to během své kariéry. Původní člen dokumentačního týmu ASP.NET, pracoval s webovými technologiemi Microsoftu po dobu dekády.

## <a name="target-audience"></a>Cílová skupina

Tato sada kurzů je určená pro vývojáře webových aplikací v ASP.NET a architekty řešení, kteří používají Visual Studio 2010 k vytváření webových aplikací na podnikové úrovni. Chcete-li získat co nejvíc hodnot z obsahu, měli byste být obeznámeni s používáním sady Visual Studio 2010 a mít základní znalost s TFS, společně s vědomím technologií webové platformy Microsoft, jako je ASP.NET MVC 3, Windows Communication Foundation (WCF), IIS, SQL. Databázové projekty serveru a sady Visual Studio. Nemusíte však být obeznámeni s nástroji a technologiemi nasazení nebo potřebujete vědět, jak nastavit systémy CI.

## <a name="requirements"></a>Požadavky

Chcete-li postupovat podle pokynů a provádět úkoly popsané v těchto kurzech, je nutné nainstalovat tento software do vašeho vývojového počítače:

- Visual Studio 2010 Premium nebo Ultimate Edition s aktualizací Service Pack 1
- .NET Framework 4,0
- .NET Framework 3,5 s aktualizací Service Pack 1
- ASP.NET MVC 3.0
- Služba IIS 7,5 Express
- SQL Server Express 2008 R2

K provedení kroků nasazení popsaných v těchto návodech budete potřebovat přístup k ukázkovým prostředím nasazení webové aplikace. Pro dosažení nejlepších výsledků by tato prostředí měla odpovídat vzoru podnikového nasazení vaší organizace. Pak můžete upravit návody poskytované v této dokumentaci, aby odrážely prostředí pro nasazení a požadavky vaší organizace.

## <a name="series-contents"></a>Obsah řady

Tento Úvodní oddíl se skládá ze dvou dalších témat. Jsou navržené tak, aby poskytovaly nějaký širší kontext pro následující kurzy:

- [Enterprise Web Deployment: Přehled scénářů](enterprise-web-deployment-scenario-overview.md). Toto téma popisuje scénář, který každý z kurzů v této sérii odkolíkuje. Scénář se zaměřuje na požadavky na správu životního cyklu aplikací (ALM) fiktivní společnosti s názvem Fabrikam, Inc., protože vyvíjí webovou aplikaci na podnikové úrovni.
- [Správa životního cyklu aplikací: od vývoje až po produkční](application-lifecycle-management-from-development-to-production.md)prostředí. Toto téma poskytuje podrobný a kompletní přehled procesu nasazení. Ukazuje, jak společnost Fabrikam, Inc. přesouvá webovou aplikaci ASP.NET na podnikové úrovni prostřednictvím testovacích, pracovních a produkčních prostředí jako součást procesu průběžného vývoje.

Řada obsahuje čtyři sady kurzů. Každá se zaměřuje na různé aspekty nasazení webu:

- [Nasazení webu v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Tento kurz obsahuje koncepční Úvod do souborů projektu MSBuild, kanál publikování na webu, Nasazení webu a další související technologie. Vysvětluje, jak můžete tyto nástroje použít společně ke správě složitých procesů nasazení.
- [Konfigurují se serverová prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). V tomto kurzu se dozvíte, jak nakonfigurovat servery Windows pro podporu různých scénářů nasazení, včetně nasazení vzdáleného webového balíčku pomocí služby Web Deployment Agent ("vzdálený agent") nebo obslužné rutiny Nasazení webu a nasazení vzdálené databáze. Poskytuje pokyny k výběru vhodné metody nasazení pro vlastní prostředí a popisuje, jak používat WFF k replikaci nasazených webových aplikací napříč všemi webovými servery v serverové farmě.
- [Konfigurace Team Foundation Server pro nasazení webu](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) V tomto kurzu se dozvíte, jak nakonfigurovat TFS pro podporu různých scénářů nasazení, včetně automatizovaného nasazení v rámci procesu CI a ruční aktivace nasazení konkrétních sestavení.
- [Pokročilé nasazení podnikového webu](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). V tomto kurzu se dozvíte, jak provádět různé pokročilejší úlohy nasazení, jako je přizpůsobení nasazení databáze pro více prostředí, vyloučení souborů a složek z nasazení a přepnutí webových aplikací do režimu offline během procesu nasazení. .

## <a name="where-to-start"></a>Kde začít

Tato sada kurzů používá ukázkové řešení s realistickým stupněm složitosti spolu se scénářem fiktivního podnikového nasazení, které poskytuje referenční implementaci a poskytuje úlohy a návody ke společnému kontextu. V dalším tématu, na [webu Enterprise Web Deployment: Přehled scénářů](enterprise-web-deployment-scenario-overview.md), se zavádí scénář a ukázkové řešení. Odtud můžete obejít kurzy a témata, které nejlépe vyhovují vašim potřebám.

> [!div class="step-by-step"]
> [Next](enterprise-web-deployment-scenario-overview.md)
