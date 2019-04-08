---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: Konfigurace serveru Team Foundation Server pro nasazení webu | Dokumentace Microsoftu
author: jrjlee
description: Tomto kurzu se dozvíte, jak nakonfigurovat Team Foundation Server (TFS) 2010 k sestavení řešení a nasazení webového obsahu do různých cílových prostředích. To...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2b668f2e9bdf73632b8b076416c9ccc5cf34a7ed
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076309"
---
<a name="configuring-team-foundation-server-for-web-deployment"></a><span data-ttu-id="5ffc1-104">Konfigurace sady Team Foundation Server pro nasazení webu</span><span class="sxs-lookup"><span data-stu-id="5ffc1-104">Configuring Team Foundation Server for Web Deployment</span></span>
====================
<span data-ttu-id="5ffc1-105">podle [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="5ffc1-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="5ffc1-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="5ffc1-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="5ffc1-107">Tomto kurzu se dozvíte, jak nakonfigurovat Team Foundation Server (TFS) 2010 k sestavení řešení a nasazení webového obsahu do různých cílových prostředích.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-107">This tutorial will show you how to configure Team Foundation Server (TFS) 2010 to build solutions and deploy web content to various target environments.</span></span> <span data-ttu-id="5ffc1-108">To zahrnuje scénáře kontinuální integrace (CI), kde nasadíte obsah automaticky pokaždé, když vývojář provádí změny.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-108">This includes continuous integration (CI) scenarios, where you deploy content automatically every time a developer makes a change.</span></span> <span data-ttu-id="5ffc1-109">Můžou také zahrnovat ruční aktivační události scénáře, ve kterém může správce k aktivaci nasazení konkrétního sestavení do přípravného prostředí po sestavení byl ověřen a ověření v testovacím prostředí.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-109">It can also include manual trigger scenarios, where an administrator may want to trigger deployment of a specific build to a staging environment once the build has been verified and validated in the test environment.</span></span> <span data-ttu-id="5ffc1-110">Témata v tomto kurzu vás provede celou konfiguraci procesu, včetně:</span><span class="sxs-lookup"><span data-stu-id="5ffc1-110">The topics in this tutorial will guide you through the entire configuration process, including:</span></span>
> 
> - <span data-ttu-id="5ffc1-111">Postup vytvoření nového týmového projektu v TFS.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-111">How to create a new team project in TFS.</span></span>
> - <span data-ttu-id="5ffc1-112">Postup přidání obsahu do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-112">How to add content to source control.</span></span>
> - <span data-ttu-id="5ffc1-113">Jak nakonfigurovat server sestavení pro podporu CI a nasazení.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-113">How to configure a build server to support CI and deployment.</span></span>
> - <span data-ttu-id="5ffc1-114">Jak vytvořit definici sestavení, která obsahuje logiku pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-114">How to create a build definition that includes deployment logic.</span></span>
> - <span data-ttu-id="5ffc1-115">Jak nakonfigurovat oprávnění pro automatické nasazení.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-115">How to configure permissions for automated deployment.</span></span>
> 
> <span data-ttu-id="5ffc1-116">Italština překlad těchto kurzů, navštivte web [ http://www.lucamorelli.it ](http://www.lucamorelli.it).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-116">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


<span data-ttu-id="5ffc1-117">Tento kurz předpokládá, že jste nainstalovali TFS 2010 a vytvoření kolekce týmových projektů jako součást počáteční konfigurace procesu.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-117">This tutorial assumes that you have installed TFS 2010 and created a team project collection as part of the initial configuration process.</span></span> <span data-ttu-id="5ffc1-118">[Team Foundation Průvodce instalací pro Visual Studio 2010](https://go.microsoft.com/?linkid=9805132) poskytuje komplexní pokyny pro tyto úlohy.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-118">The [Team Foundation Installation Guide for Visual Studio 2010](https://go.microsoft.com/?linkid=9805132) provides comprehensive guidance on these tasks.</span></span>

## <a name="context"></a><span data-ttu-id="5ffc1-119">Kontext</span><span class="sxs-lookup"><span data-stu-id="5ffc1-119">Context</span></span>

<span data-ttu-id="5ffc1-120">To je součástí série kurzů na základě požadavků organizace nasazení fiktivní společnosti s názvem společnosti Fabrikam, Inc. V této sérii kurzů používá ukázkové řešení&#x2014; [Správce kontaktů](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) řešení&#x2014;představující webovou aplikaci s realistické úroveň složitosti, včetně aplikace ASP.NET MVC 3, komunikace Windows Služba Foundation (WCF) a databázový projekt.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-120">This forms part of a series of tutorials based on the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="5ffc1-121">Metody nasazení v srdci těchto kurzů je založen na rozdělení přístupu soubor projektu je popsáno v [Principy procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md), ve které je řízena procesem sestavení dva soubory projektu&#x2014;jeden obsahující pokyny, které platí pro všechny cílové prostředí a jeden obsahuje nastavení pro konkrétní prostředí sestavení a nasazení pro sestavení.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-121">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="5ffc1-122">V okamžiku sestavení souboru projektu specifických pro prostředí se sloučí do souboru projektu bez ohledu na prostředí a vytvoří kompletní sadu pokynů sestavení.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-122">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="5ffc1-123">Přehledný scénář</span><span class="sxs-lookup"><span data-stu-id="5ffc1-123">Scenario Overview</span></span>

<span data-ttu-id="5ffc1-124">Základní scénář pro tyto kurzy je popsaný v [nasazení podnikového webu: Přehled scénářů](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-124">The high-level scenario for these tutorials is described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span></span> <span data-ttu-id="5ffc1-125">Doporučujeme, abyste si toto téma před zahájením práce v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-125">We recommend that you review this topic before you get started on this tutorial.</span></span>

## <a name="how-to-use-this-tutorial"></a><span data-ttu-id="5ffc1-126">Jak používat v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="5ffc1-126">How to Use This Tutorial</span></span>

<span data-ttu-id="5ffc1-127">Pokud je to první úkoly popsané v tomto kurzu jste provedli, nebo pokud chcete postupovat podle příkladů použití ukázkové řešení, měli nejdřív projít témata kurzu v pořadí.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-127">If this is the first time you've performed the tasks described in this tutorial, or if you want to follow the examples using the sample solution, you should work through the tutorial topics in order.</span></span> <span data-ttu-id="5ffc1-128">Alternativně můžete použít jednotlivých tématech jako pokyny pro konkrétní úlohy.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-128">Alternatively, you can use individual topics as guidance for specific tasks.</span></span> <span data-ttu-id="5ffc1-129">Tento kurz obsahuje následující témata:</span><span class="sxs-lookup"><span data-stu-id="5ffc1-129">This tutorial includes these topics:</span></span>

- <span data-ttu-id="5ffc1-130">[Vytvoření týmového projektu v TFS](creating-a-team-project-in-tfs.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-130">[Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span> <span data-ttu-id="5ffc1-131">Týmový projekt je základní jednotkou správy zdrojového kódu, řízení procesů a sestavení v TFS.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-131">A team project is the core unit for source control, process management, and build in TFS.</span></span> <span data-ttu-id="5ffc1-132">Potřebujete vytvořit týmový projekt, než budete moct přidat obsah do správy zdrojového kódu nebo vytváření definice sestavení.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-132">You need to create a team project before you can add content to source control or create build definitions.</span></span>
- <span data-ttu-id="5ffc1-133">[Přidávání obsahu do správy zdrojových kódů](adding-content-to-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-133">[Adding Content to Source Control](adding-content-to-source-control.md).</span></span> <span data-ttu-id="5ffc1-134">Po vytvoření týmového projektu, můžete začít přidávat obsah do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-134">Once you've created a team project, you can start adding content to source control.</span></span> <span data-ttu-id="5ffc1-135">Bude potřeba přidat projekty a řešení, společně s externích závislostí, před zahájením konfigurace sestavení.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-135">You'll need to add your projects and solutions, together with any external dependencies, before you can start configuring builds.</span></span>
- <span data-ttu-id="5ffc1-136">[Konfigurace serveru TFS Server sestavení pro nasazení webu](configuring-a-tfs-build-server-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-136">[Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span> <span data-ttu-id="5ffc1-137">Pokud chcete k sestavení obsahu vašeho týmu projektu, budete potřebovat ke konfiguraci serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-137">If you want to build your team project content, you'll need to configure a build server.</span></span> <span data-ttu-id="5ffc1-138">Ve většině případů by měl být na samostatném počítači z instalace TFS.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-138">In most cases, this should be on a separate machine from your TFS installation.</span></span> <span data-ttu-id="5ffc1-139">Ke konfiguraci serveru sestavení, je potřeba nainstalovat a nakonfigurovat službu sestavení TFS, nainstalujte Visual Studio 2010, vytvořit kontrolery sestavení a agenty sestavení, nainstalovat všechny produkty nebo komponenty, které váš kód potřebuje, aby bylo možné úspěšně sestavit a nainstalovat Internetová informační služba (IIS) webu nástroj pro nasazení (Web Deploy).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-139">To configure a build server, you need to install and configure the TFS build service, install Visual Studio 2010, create build controllers and build agents, install any products or components that your code needs in order to build successfully, and install the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="5ffc1-140">[Vytvoření definice sestavení, která podporuje nasazení](creating-a-build-definition-that-supports-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-140">[Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="5ffc1-141">Před zahájením zařazování do fronty a budou spouštět buildy na serveru TFS, je potřeba vytvořit definice alespoň jedno sestavení pro týmový projekt.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-141">Before you can start queuing or triggering builds in TFS, you need to create at least one build definition for your team project.</span></span> <span data-ttu-id="5ffc1-142">Definice sestavení definuje každý aspekt sestavení, včetně věci, které by měl být součástí sestavení, co by měly aktivovat sestavení a kam by měl Team Build poslat výstupy sestavení.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-142">The build definition defines every aspect of the build, including which things should be included in the build, what should trigger the build, and where Team Build should send the build outputs.</span></span> <span data-ttu-id="5ffc1-143">Můžete nakonfigurovat definici sestavení spouštět vlastní soubory projektu Microsoft Build Engine (MSBuild), která umožňuje zahrnout logiky nasazení v automatizovaných sestaveních.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-143">You can configure a build definition to run custom Microsoft Build Engine (MSBuild) project files, which lets you include deployment logic in your automated builds.</span></span>
- <span data-ttu-id="5ffc1-144">[Nasazení konkrétního sestavení](deploying-a-specific-build.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-144">[Deploying a Specific Build](deploying-a-specific-build.md).</span></span> <span data-ttu-id="5ffc1-145">V možných scénářů budete chtít nasazení konkrétního sestavení, nikoli na nejnovější verzi na cílovém prostředí.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-145">In a lot of scenarios, you'll want to deploy a specific build, rather than the latest build, to a target environment.</span></span> <span data-ttu-id="5ffc1-146">V takovém případě můžete nakonfigurovat definici sestavení, která nasadí obsah z konkrétní odkládací složky.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-146">In this case, you can configure a build definition that deploys content from a specific drop folder.</span></span>
- <span data-ttu-id="5ffc1-147">[Nasazení sestavení konfigurace oprávnění pro tým](configuring-permissions-for-team-build-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-147">[Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md).</span></span> <span data-ttu-id="5ffc1-148">Pokud je sestavovací služba pro nasazení obsahu jako součást automatizovaného procesu sestavení, budete muset poskytnout různá oprávnění k účtu sestavovací služby na všechny cílové webové servery a databázové servery.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-148">If the build service is to deploy content as part of an automated build process, you need to grant various permissions to the build service account on any destination web servers and database servers.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="5ffc1-149">Klíčové technologie</span><span class="sxs-lookup"><span data-stu-id="5ffc1-149">Key Technologies</span></span>

<span data-ttu-id="5ffc1-150">Tento kurz se zaměřuje na tom, jak používat tyto produkty a technologie pro podporu automatické sestavení a nasazení webu:</span><span class="sxs-lookup"><span data-stu-id="5ffc1-150">This tutorial focuses on how to use these products and technologies to support automated build and web deployment:</span></span>

- <span data-ttu-id="5ffc1-151">Visual Studio Team Foundation Server 2010</span><span class="sxs-lookup"><span data-stu-id="5ffc1-151">Visual Studio Team Foundation Server 2010</span></span>
- <span data-ttu-id="5ffc1-152">Týmové sestavení a nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="5ffc1-152">Team Build and MSBuild</span></span>
- <span data-ttu-id="5ffc1-153">Web Deploy</span><span class="sxs-lookup"><span data-stu-id="5ffc1-153">Web Deploy</span></span>

<span data-ttu-id="5ffc1-154">Tento kurz se dotýká také při použití Windows serveru 2008 R2, IIS 7.5, SQL Server 2008 R2, technologii ASP.NET 4.0 a ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-154">The tutorial also touches on the use of Windows Server 2008 R2, IIS 7.5, SQL Server 2008 R2, ASP.NET 4.0, and ASP.NET MVC 3.</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="5ffc1-155">Další kurzy v této sérii</span><span class="sxs-lookup"><span data-stu-id="5ffc1-155">Other Tutorials in This Series</span></span>

<span data-ttu-id="5ffc1-156">To je součástí série pěti kurzů na podnikové úrovni, nasazení webu.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-156">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="5ffc1-157">Toto jsou další kurzy v této sérii:</span><span class="sxs-lookup"><span data-stu-id="5ffc1-157">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="5ffc1-158">[Nasazení webové aplikace v podnikových scénářích](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-158">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="5ffc1-159">Tento úvodní obsah obsahuje kontextové informace týkající se série kurzů.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-159">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="5ffc1-160">Popisuje scénář tohoto kurzu a ukazuje, jak se úlohy a názorné postupy popsané v celé řadě vejde do širší proces správy životního cyklu aplikací (ALM).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-160">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="5ffc1-161">[Webové nasazení v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-161">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="5ffc1-162">Tento kurz obsahuje koncepční Úvod do souborů projektu MSBuild, webových publikování kanálu (WPP), nasazení webu a dalších souvisejících technologiích.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-162">This tutorial provides a conceptual introduction to MSBuild project files, the Web Publishing Pipeline (WPP), Web Deploy, and other related technologies.</span></span> <span data-ttu-id="5ffc1-163">Vysvětluje, jak můžete pomocí těchto nástrojů společně ke správě nasazení komplexních procesů.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-163">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="5ffc1-164">[Konfigurace serverového prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-164">[Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span> <span data-ttu-id="5ffc1-165">Tento kurz popisuje, jak nakonfigurovat servery Windows pro podporu různých scénářů nasazení, včetně nasazení vzdáleného webového balíčku pomocí Služba agenta nasazení webu (vzdálený agent) nebo obslužná rutina webového nasazení a nasazení vzdálené databáze.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-165">This tutorial describes how to configure Windows servers to support various deployment scenarios, including remote web package deployment using the Web Deployment Agent Service (the remote agent) or the Web Deploy Handler and remote database deployment.</span></span> <span data-ttu-id="5ffc1-166">Poskytuje rady, jak volba metody nasazení pro konkrétní prostředí, a je zde popsán způsob použít webové farmy Framework (WFF) k replikaci nasazených webových aplikací ve všech webových serverů v serverové farmě.</span><span class="sxs-lookup"><span data-stu-id="5ffc1-166">It provides guidance on choosing the appropriate deployment method for your own environment, and it describes how to use the Web Farm Framework (WFF) to replicate deployed web applications across all the web servers in a server farm.</span></span>
- <span data-ttu-id="5ffc1-167">[Pokročilé nasazení podnikového webu](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5ffc1-167">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="5ffc1-168">Tento kurz popisuje, jak k provádění různých rozšířené nasazení úkoly, jako je přizpůsobení nasazené databáze pro více prostředí, s výjimkou souborů a složek z nasazení a převedení webové aplikace do offline režimu během procesu nasazení .</span><span class="sxs-lookup"><span data-stu-id="5ffc1-168">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5ffc1-169">Next</span><span class="sxs-lookup"><span data-stu-id="5ffc1-169">Next</span></span>](creating-a-team-project-in-tfs.md)