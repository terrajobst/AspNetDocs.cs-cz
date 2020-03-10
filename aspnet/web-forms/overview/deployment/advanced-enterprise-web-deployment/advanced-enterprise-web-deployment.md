---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
title: Nasazení webu Advanced Enterprise | Microsoft Docs
author: jrjlee
description: V tomto kurzu se dozvíte, jak ve velkých scénářích podnikového nasazení provádět různé úkoly, které jsou nutné nebo vhodné. Pro italské překlady...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 7dcaba80-f2ec-4db3-ad98-daadc3afdb49
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: bf4c7d021763017592483df35cb717295c4924aa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587603"
---
# <a name="advanced-enterprise-web-deployment"></a>Pokročilé nasazení podnikového webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> V tomto kurzu se dozvíte, jak ve velkých scénářích podnikového nasazení provádět různé úkoly, které jsou nutné nebo vhodné.
> 
> Pro účely nizozemského překladu těchto kurzů navštivte [http://www.lucamorelli.it](http://www.lucamorelli.it).

Tato část je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého řešení [](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) &#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto výukových programů je založena na způsobu sestavení rozděleného projektu popsaných v tématu [Principy procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="scenario-overview"></a>Přehled scénáře

Scénář vysoké úrovně pro tyto kurzy je popsaný v tématu [Přehled podnikového nasazení webu: scénář](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md). Doporučujeme, abyste si před zahájením tohoto kurzu Přečtěte toto téma.

## <a name="how-to-use-this-tutorial"></a>Jak používat tento kurz

- Všechna témata v tomto kurzu jsou samostatně obsažená a řeší konkrétní výzvu nebo problém, ke kterým dochází ve scénářích podnikového nasazení. Tato témata nemusíte v žádném konkrétním pořadí používat. V tomto kurzu se ale zabývá několik pokročilých úloh. V takovém případě byste se měli seznámit s koncepty a technikami, které [nasazení webu v podnikovém](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md) kurzu pokrývá, aby bylo možné získat z tohoto obsahu nejvíc výhod.
- Tento kurz obsahuje tato témata:
- [Probíhá nasazení "What If"](performing-a-what-if-deployment.md). V mnoha scénářích budete chtít určit dopad navrhovaného nasazení v cílovém prostředí nebo jakémkoli existujícím obsahu, abyste mohli skutečně provést změny. V tomto tématu se dozvíte, jak můžete spustit nasazení "Co když", aby se generovaly soubory protokolu a skripty aktualizace databáze, jako kdyby jste nasadili obsah do cílového prostředí, aniž byste museli provádět žádné změny. Analýza těchto prostředků vám může přispět k navýšení potenciálních problémů předem při živém nasazení.
- [Přizpůsobení nasazení databáze pro více prostředí](customizing-database-deployments-for-multiple-environments.md). Když nasadíte databázový projekt do více cílů, často budete chtít přizpůsobit vlastnosti nasazení pro každé cílové prostředí. Například v testovacích prostředích byste při každém nasazení obvykle znovu vytvořili databázi, zatímco v pracovních nebo produkčních prostředích byste měli větší mnohem více pravděpodobných přírůstkových aktualizací, abyste zachovali data. Toto téma popisuje, jak můžete začlenit tyto změny vlastností do logiky nasazení vytvořením souboru konfigurace nasazení specifického pro prostředí (. SqlDeployment) pro každé cílové prostředí.
- Nasazování členství databázové role do testovacích prostředí. Při opětovném vytvoření databáze pro každé nasazení&#x2014;například jako součást sestavení průběžné integrace (CI) a nasazení do testovacího prostředí&#x2014;budete obvykle muset nakonfigurovat členství databázových rolí pokaždé. Obvykle budete muset udělit oprávnění identitě fondu aplikací, které jsou přidružené k vaší webové aplikaci. Toto téma popisuje, jak tento proces můžete automatizovat přidáním skriptu SQL po nasazení do logiky nasazení.
- [Nasazení databází členství v podnikových prostředích](deploying-membership-databases-to-enterprise-environments.md). Databáze členství v ASP.NET mají různé charakteristiky, které mohou zkomplikovat proces nasazení. Například nasazení pouze ze schématu ponechá databázi v nefunkčním stavu. Ve většině scénářů je vhodnější vytvořit databázi členství přímo v každém cílovém prostředí. Pokud ale potřebujete nasadit databázi členství, toto téma popisuje některé z přístupů, které můžete použít ke splnění základních problémů.
- [Vyloučení souborů a složek z nasazení](excluding-files-and-folders-from-deployment.md). V některých scénářích budete chtít obsah svého webového balíčku přizpůsobit konkrétním cílovým prostředím. Například můžete chtít zahrnout plné verze knihoven JavaScriptu při nasazení do testovacího prostředí, pro podporu ladění na straně klienta, ale při nasazení do pracovního nebo produkčního prostředí používat minifikovaného verze knihoven. Toto téma popisuje, jak můžete z procesu vytváření balíčku vyloučit konkrétní soubory a složky.
- [Přepnutí webových aplikací do režimu offline pomocí nasazení webu](taking-web-applications-offline-with-web-deploy.md). Když nasadíte řešení do pracovního nebo produkčního prostředí, často budete chtít své webové aplikace převést do režimu offline po dobu trvání procesu nasazení. Toto téma popisuje, jak můžete přidat *aplikaci\_offline souboru. htm* do webové aplikace na začátku procesu nasazení a odebrat ho na konci. I když je *aplikace\_offline souboru. htm* , všichni uživatelé, kteří procházejí webovou aplikaci, budou automaticky přesměrováni do souboru *\_offline. htm aplikace* .
- [Spouštění skriptů prostředí Windows PowerShell z nástroje MSBuild](running-windows-powershell-scripts-from-msbuild-project-files.md). Mnoho scénářů nasazení vyžaduje složitější akce po nasazení, jako je přidání vlastních zdrojů událostí do registru nebo konfigurace replikace mezi instancemi SQL Server. Tyto akce jsou často prováděny pomocí skriptů prostředí Windows PowerShell. Toto téma popisuje, jak spustit skripty prostředí Windows PowerShell ze souboru projektu Microsoft Build Engine (MSBuild) jako součást procesu sestavení a nasazení.
- [Řešení potíží s procesem balení](troubleshooting-the-packaging-process.md). Kanál pro publikování na webu (WPP) definuje vlastnost MSBuild s názvem **EnablePackageProcessLoggingAndAssert** , kterou můžete použít ke generování podrobných informací o procesu balení pro projekty webových aplikací. Toto téma popisuje, co dělá vlastnost a jak ji používat.

## <a name="key-technologies"></a>Klíčové technologie

Tento kurz se zaměřuje na použití těchto produktů a technologií k podpoře automatizovaného sestavení a nasazení webu:

- Visual Studio 2010 and Team Foundation Server (TFS) 2010
- Sestavení týmu pro MSBuild a TFS
- Internetová informační služba (IIS) 7,5
- Nástroj pro nasazení webu služby IIS (Nasazení webu) 2,1
- Nástroj pro nasazení databáze VSDBCMD. exe

## <a name="other-tutorials-in-this-series"></a>Další kurzy v této řadě

Tato část tvoří řadu pěti kurzů pro nasazení webu na podnikové úrovni. Toto jsou další kurzy v řadě:

- [Nasazení webových aplikací v podnikových scénářích](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Tento úvodní obsah poskytuje kontextové pozadí pro řadu kurzů. Popisuje scénář kurzu a ukazuje, jak se úlohy a návody popsané v rámci řady vešly do širšího procesu správy životního cyklu aplikací (ALM).
- [Nasazení webu v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Tento kurz obsahuje koncepční Úvod do souborů projektu MSBuild, WPP, Nasazení webu a další související technologie. Vysvětluje, jak můžete tyto nástroje použít společně ke správě složitých procesů nasazení.
- [Konfigurují se serverová prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). V tomto kurzu se dozvíte, jak nakonfigurovat servery Windows pro podporu různých scénářů nasazení, včetně nasazení vzdáleného webového balíčku pomocí služby Web Deployment Agent Service (vzdálený Agent) nebo obslužné rutiny Nasazení webu a nasazení vzdálené databáze. Poskytuje pokyny k výběru vhodné metody nasazení pro vlastní prostředí a popisuje, jak používat webové serverové farmy (WFF) k replikaci nasazených webových aplikací napříč všemi webovými servery v serverové farmě.
- [Konfigurace Team Foundation Server pro nasazení webu](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) V tomto kurzu se dozvíte, jak nakonfigurovat TFS pro podporu různých scénářů nasazení, včetně automatizovaného nasazení v rámci procesu CI a ruční aktivace nasazení konkrétních sestavení.

> [!div class="step-by-step"]
> [Next](performing-a-what-if-deployment.md)
