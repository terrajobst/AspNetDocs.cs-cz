---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: Konfigurace Team Foundation Server pro nasazení webu | Microsoft Docs
author: jrjlee
description: V tomto kurzu se dozvíte, jak nakonfigurovat Team Foundation Server (TFS) 2010 k vytváření řešení a nasazení webového obsahu do různých cílových prostředí. ...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 638d696abbc5f05957c0ed2eb7ebb65fce7813ea
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528390"
---
# <a name="configuring-team-foundation-server-for-web-deployment"></a>Konfigurace sady Team Foundation Server pro nasazení webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> V tomto kurzu se dozvíte, jak nakonfigurovat Team Foundation Server (TFS) 2010 k vytváření řešení a nasazení webového obsahu do různých cílových prostředí. To zahrnuje scénáře průběžné integrace (CI), kde se obsah automaticky nasazuje při každé změně vývojáře. Může také zahrnovat scénáře ručních triggerů, kde správce může chtít aktivovat nasazení konkrétního sestavení do přípravného prostředí po ověření a ověření sestavení v testovacím prostředí. Témata v tomto kurzu vás provedou celým procesem konfigurace, včetně:
> 
> - Postup vytvoření nového týmového projektu v TFS.
> - Postup přidání obsahu do správy zdrojového kódu.
> - Jak nakonfigurovat server sestavení pro podporu CI a nasazení.
> - Jak vytvořit definici sestavení, která zahrnuje logiku nasazení.
> - Jak nakonfigurovat oprávnění pro automatizované nasazení.
> 
> Pro účely nizozemského překladu těchto kurzů navštivte [http://www.lucamorelli.it](http://www.lucamorelli.it).

V tomto kurzu se předpokládá, že máte nainstalovanou sadu TFS 2010 a vytvořili jste kolekci týmového projektu jako součást procesu počáteční konfigurace. [Průvodce instalací Team Foundation pro Visual Studio 2010](https://go.microsoft.com/?linkid=9805132) poskytuje komplexní pokyny k těmto úlohám.

## <a name="context"></a>Kontext

Tato část je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého řešení [](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) &#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto výukových programů je založena na způsobu sestavení rozděleného projektu popsaných v tématu [Principy procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="scenario-overview"></a>Přehled scénáře

Scénář vysoké úrovně pro tyto kurzy je popsaný v tématu [Přehled podnikového nasazení webu: scénář](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md). Doporučujeme, abyste si před zahájením tohoto kurzu Přečtěte toto téma.

## <a name="how-to-use-this-tutorial"></a>Jak používat tento kurz

Pokud se jedná o první kroky popsané v tomto kurzu, nebo pokud chcete postupovat podle příkladů pomocí ukázkového řešení, měli byste pracovat prostřednictvím témat kurzu v uvedeném pořadí. Alternativně můžete použít jednotlivá témata jako pokyny pro konkrétní úkoly. Tento kurz obsahuje tato témata:

- [Vytvoření týmového projektu v TFS](creating-a-team-project-in-tfs.md). Týmový projekt je základní jednotkou pro správu zdrojového kódu, správu procesů a sestavení v TFS. Musíte vytvořit týmový projekt, abyste mohli přidat obsah do správy zdrojových kódů nebo vytvořit definice sestavení.
- [Přidávání obsahu do správy zdrojového kódu](adding-content-to-source-control.md). Po vytvoření týmového projektu můžete začít přidávat obsah do správy zdrojového kódu. Než začnete konfigurovat buildy, budete muset přidat své projekty a řešení společně s případnými externími závislostmi.
- [Konfigurace serveru sestavení TFS pro nasazení webu](configuring-a-tfs-build-server-for-web-deployment.md). Pokud chcete sestavit obsah týmového projektu, budete muset nakonfigurovat server sestavení. Ve většině případů by to mělo být v samostatném počítači z instalace TFS. Chcete-li konfigurovat server sestavení, je nutné nainstalovat a nakonfigurovat sestavovací službu TFS, nainstalovat sadu Visual Studio 2010, vytvořit řadiče sestavení a agenty sestavení, nainstalovat všechny produkty nebo komponenty, které váš kód potřebuje k úspěšnému sestavení, a nainstalovat Nástroj pro nasazení webu Internetová informační služba (IIS) (Nasazení webu).
- [Vytvoření definice sestavení, která podporuje nasazení](creating-a-build-definition-that-supports-deployment.md). Než budete moci spustit zařazování do fronty nebo aktivovat sestavení v TFS, je nutné vytvořit alespoň jednu definici sestavení pro týmový projekt. Definice sestavení definuje všechny aspekty sestavení, včetně toho, které by měly být zahrnuty do sestavení, co by mělo aktivovat sestavení a kde má sestavení týmu odeslat výstupy sestavení. Můžete nakonfigurovat definici sestavení, aby spouštěla vlastní soubory projektu Microsoft Build Engine (MSBuild), které vám umožní zahrnout do automatizovaných sestavení logiku nasazení.
- [Nasazení konkrétního sestavení](deploying-a-specific-build.md). V mnoha scénářích budete chtít nasadit konkrétní sestavení místo nejnovějšího sestavení do cílového prostředí. V takovém případě můžete nakonfigurovat definici sestavení, která nasadí obsah z konkrétní ukládací složky.
- [Konfigurace oprávnění pro nasazení týmového sestavení](configuring-permissions-for-team-build-deployment.md). Pokud sestavovací služba slouží k nasazení obsahu v rámci procesu automatizovaného sestavení, je nutné udělit účtu služby sestavení různá oprávnění na všech cílových webových serverech a databázových serverech.

## <a name="key-technologies"></a>Klíčové technologie

Tento kurz se zaměřuje na použití těchto produktů a technologií k podpoře automatizovaného sestavení a nasazení webu:

- Visual Studio Team Foundation Server 2010
- Sestavení týmu a MSBuild
- Nasazení webu

Tento kurz se taky dotýká použití Windows serveru 2008 R2, IIS 7,5, SQL Server 2008 R2, ASP.NET 4,0 a ASP.NET MVC 3.

## <a name="other-tutorials-in-this-series"></a>Další kurzy v této řadě

Tato část tvoří řadu pěti kurzů pro nasazení webu na podnikové úrovni. Toto jsou další kurzy v řadě:

- [Nasazení webových aplikací v podnikových scénářích](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Tento úvodní obsah poskytuje kontextové pozadí pro řadu kurzů. Popisuje scénář kurzu a ukazuje, jak se úlohy a návody popsané v rámci řady vešly do širšího procesu správy životního cyklu aplikací (ALM).
- [Nasazení webu v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). V tomto kurzu se seznámíte s koncepčním úvodem do souborů projektu MSBuild, kanálu pro web publikování (WPP), Nasazení webu a dalších souvisejících technologií. Vysvětluje, jak můžete tyto nástroje použít společně ke správě složitých procesů nasazení.
- [Konfigurují se serverová prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). V tomto kurzu se dozvíte, jak nakonfigurovat servery Windows pro podporu různých scénářů nasazení, včetně nasazení vzdáleného webového balíčku pomocí služby Web Deployment Agent Service (vzdálený Agent) nebo obslužné rutiny Nasazení webu a nasazení vzdálené databáze. Poskytuje pokyny k výběru vhodné metody nasazení pro vlastní prostředí a popisuje, jak používat webové serverové farmy (WFF) k replikaci nasazených webových aplikací napříč všemi webovými servery v serverové farmě.
- [Pokročilé nasazení podnikového webu](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). V tomto kurzu se dozvíte, jak provádět různé pokročilejší úlohy nasazení, jako je přizpůsobení nasazení databáze pro více prostředí, vyloučení souborů a složek z nasazení a přepnutí webových aplikací do režimu offline během procesu nasazení. .

> [!div class="step-by-step"]
> [Next](creating-a-team-project-in-tfs.md)
