---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: Konfigurace serveru TFS Server sestavení pro nasazení webu | Dokumentace Microsoftu
author: jrjlee
description: Toto téma popisuje, jak připravit server sestavení Team Foundation Server (TFS) k vytvoření a nasazení řešení s využitím Team Build nebo Informat Internetu...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 534a0edf5c26dd2daec3c44e41410f8c5de96c15
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076093"
---
<a name="configuring-a-tfs-build-server-for-web-deployment"></a><span data-ttu-id="e9617-103">Konfigurace serveru TFS Build pro nasazení webu</span><span class="sxs-lookup"><span data-stu-id="e9617-103">Configuring a TFS Build Server for Web Deployment</span></span>
====================
<span data-ttu-id="e9617-104">podle [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="e9617-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="e9617-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="e9617-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="e9617-106">Toto téma popisuje, jak připravit server sestavení Team Foundation Server (TFS) k vytvoření a nasazení řešení s využitím týmové sestavení a nástroj pro nasazení Internetové informační služby (IIS) webu (nasazení webu).</span><span class="sxs-lookup"><span data-stu-id="e9617-106">This topic describes how to prepare a Team Foundation Server (TFS) build server to build and deploy your solutions using Team Build and the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>


<span data-ttu-id="e9617-107">Toto téma je součástí série kurzů podle požadavků na nasazení enterprise fiktivní společnosti s názvem společnosti Fabrikam, Inc. V této sérii kurzů používá ukázkové řešení&#x2014; [řešení Správce kontaktů](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;představující webovou aplikaci s realistické úroveň složitosti, včetně aplikace ASP.NET MVC 3, komunikace Windows Služba Foundation (WCF) a databázový projekt.</span><span class="sxs-lookup"><span data-stu-id="e9617-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="e9617-108">Metody nasazení v srdci těchto kurzů je založen na rozdělení přístupu soubor projektu je popsáno v [vysvětlení souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve které je řízena procesem sestavení dva soubory projektu&#x2014;jeden obsahující pokyny, které platí pro všechny cílové prostředí a jeden obsahuje nastavení pro konkrétní prostředí sestavení a nasazení pro sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="e9617-109">V okamžiku sestavení souboru projektu specifických pro prostředí se sloučí do souboru projektu bez ohledu na prostředí a vytvoří kompletní sadu pokynů sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="e9617-110">Přehled úloh</span><span class="sxs-lookup"><span data-stu-id="e9617-110">Task Overview</span></span>

<span data-ttu-id="e9617-111">Pokud chcete připravit server sestavení k sestavení a nasazení vašeho řešení, bude nutné:</span><span class="sxs-lookup"><span data-stu-id="e9617-111">To prepare a build server to build and deploy your solutions, you'll need to:</span></span>

- <span data-ttu-id="e9617-112">Instalace a konfigurace služby sestavení serveru TFS.</span><span class="sxs-lookup"><span data-stu-id="e9617-112">Install and configure the TFS build service.</span></span>
- <span data-ttu-id="e9617-113">Install Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="e9617-113">Install Visual Studio 2010.</span></span>
- <span data-ttu-id="e9617-114">Nainstalujte všechny produkty nebo komponenty, které jsou nutné k vytvoření řešení, jako je verze rozhraní .NET Framework nebo technologie ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e9617-114">Install any products or components that are required to build your solution, like versions of the .NET Framework or ASP.NET MVC.</span></span>
- <span data-ttu-id="e9617-115">Nainstalujte nástroj nasazení webu 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="e9617-115">Install Web Deploy 2.0 or later.</span></span>

<span data-ttu-id="e9617-116">Toto téma se ukazují, jak provést tyto postupy nebo ukazovaly na další zdroje, pokud existují.</span><span class="sxs-lookup"><span data-stu-id="e9617-116">This topic will show you how to perform these procedures or point to other resources where they exist.</span></span> <span data-ttu-id="e9617-117">Úlohy a názorné postupy v tomto tématu se předpokládá, že:</span><span class="sxs-lookup"><span data-stu-id="e9617-117">The tasks and walkthroughs in this topic assume that:</span></span>

- <span data-ttu-id="e9617-118">Začínáte s čisté server sestavení spuštěn Windows Server 2008 R2 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="e9617-118">You're starting with a clean server build running Windows Server 2008 R2 Service Pack 1.</span></span>
- <span data-ttu-id="e9617-119">Server není připojený k doméně se statickou IP adresou.</span><span class="sxs-lookup"><span data-stu-id="e9617-119">The server is domain-joined with a static IP address.</span></span>
- <span data-ttu-id="e9617-120">Jste nainstalovali aplikační vrstvu TFS na samostatném serveru, jak je popsáno v [nasazení podnikového webu: Přehled scénářů](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9617-120">You've installed the TFS application tier on a separate server, as described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="e9617-121">Kdo provádí tyto postupy?</span><span class="sxs-lookup"><span data-stu-id="e9617-121">Who Performs These Procedures?</span></span>

<span data-ttu-id="e9617-122">Ve většině případů bude zodpovědná za konfiguraci serverů sestavení správcem serveru TFS.</span><span class="sxs-lookup"><span data-stu-id="e9617-122">In most cases, a TFS administrator will be responsible for configuring build servers.</span></span> <span data-ttu-id="e9617-123">V některých případech vývojovému týmu může převzít vlastnictví servery konkrétního sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-123">In some cases, the developer team may take ownership of specific build servers.</span></span>

## <a name="install-and-configure-the-tfs-build-service"></a><span data-ttu-id="e9617-124">Instalace a konfigurace služby sestavení TFS</span><span class="sxs-lookup"><span data-stu-id="e9617-124">Install and Configure the TFS Build Service</span></span>

<span data-ttu-id="e9617-125">Při konfiguraci serveru sestavení, je první úkol k instalaci a konfiguraci služby sestavení serveru TFS.</span><span class="sxs-lookup"><span data-stu-id="e9617-125">When you configure a build server, your first task is to install and configure the TFS build service.</span></span> <span data-ttu-id="e9617-126">Jako součást tohoto procesu bude potřeba:</span><span class="sxs-lookup"><span data-stu-id="e9617-126">As part of this process, you'll need to:</span></span>

- <span data-ttu-id="e9617-127">Nainstalovat službu sestavení sady TFS a nakonfigurovat účet služby.</span><span class="sxs-lookup"><span data-stu-id="e9617-127">Install the TFS build service and configure a service account.</span></span> <span data-ttu-id="e9617-128">Všechny úlohy sestavení, včetně nasazení, se spustí pomocí identity účtu služby sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-128">Any build tasks, including deployment, will run using the identity of the build service account.</span></span>
- <span data-ttu-id="e9617-129">Vytvoření *kontrolér sestavení* a jeden nebo více *sestavovací agenty*.</span><span class="sxs-lookup"><span data-stu-id="e9617-129">Create a *build controller* and one or more *build agents*.</span></span> <span data-ttu-id="e9617-130">Každý kontrolér sestavení spravuje sadu agentů sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-130">Each build controller manages a set of build agents.</span></span> <span data-ttu-id="e9617-131">Při sestavení do fronty, kontrolér sestavení úlohu sestavení přiřadí agenta sestavení k dispozici.</span><span class="sxs-lookup"><span data-stu-id="e9617-131">When you queue a build, the build controller assigns the build task to an available build agent.</span></span> <span data-ttu-id="e9617-132">Každou kolekci týmových projektů v TFS je namapován na jeden řadič sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-132">Each team project collection in TFS is mapped to a single build controller.</span></span>
- <span data-ttu-id="e9617-133">Nakonfigurujte odkládací složky pro vaše výstupy sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-133">Configure a drop folder for your build outputs.</span></span> <span data-ttu-id="e9617-134">Toto je sdílené síťové složky.</span><span class="sxs-lookup"><span data-stu-id="e9617-134">This is a network share.</span></span> <span data-ttu-id="e9617-135">Všechny výstupy, jako jsou balíčky webového nasazení sestavení, jsou odeslány do odkládací složky.</span><span class="sxs-lookup"><span data-stu-id="e9617-135">Any build outputs, like web deployment packages, are sent to the drop folder.</span></span>

<span data-ttu-id="e9617-136">[Správa Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx) kapitoly na webové stránce MSDN obsahuje všechny prostředky, které potřebují k vykonávání těchto úkolů:</span><span class="sxs-lookup"><span data-stu-id="e9617-136">The [Administering Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx) chapter on MSDN contains all the resources you need in order to perform these tasks:</span></span>

- <span data-ttu-id="e9617-137">Koncepční přehled služby Team Foundation Build, včetně služby build service, kontrolery sestavení a agenty sestavení, viz [Principy systému sestavení Team Foundation](https://msdn.microsoft.com/library/dd793166.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9617-137">For a conceptual overview of Team Foundation Build, including the build service, build controllers, and build agents, see [Understanding a Team Foundation Build System](https://msdn.microsoft.com/library/dd793166.aspx).</span></span>
- <span data-ttu-id="e9617-138">Informace o instalaci a konfiguraci služby sestavení najdete v tématu [konfigurace sestavení počítače](https://msdn.microsoft.com/library/ms181712.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9617-138">For information on installing and configuring the build service, see [Configure a Build Machine](https://msdn.microsoft.com/library/ms181712.aspx).</span></span>
- <span data-ttu-id="e9617-139">Informace o vytváření kontrolery sestavení naleznete v tématu [Create and Work s řadičem sestavení](https://msdn.microsoft.com/library/ee330987.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9617-139">For information on creating build controllers, see [Create and Work with a Build Controller](https://msdn.microsoft.com/library/ee330987.aspx).</span></span>
- <span data-ttu-id="e9617-140">Informace o vytváření sestavovacích agentů najdete v tématu [Create and Work s agenty sestavení](https://msdn.microsoft.com/library/bb399135.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9617-140">For information on creating build agents, see [Create and Work with Build Agents](https://msdn.microsoft.com/library/bb399135.aspx).</span></span>
- <span data-ttu-id="e9617-141">Informace o vytváření a nastavení odkládacích složek, najdete v tématu [nastavit až vyřadit složky](https://msdn.microsoft.com/library/bb778394.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9617-141">For information on creating and configuring drop folders, see [Set Up Drop Folders](https://msdn.microsoft.com/library/bb778394.aspx).</span></span>

## <a name="install-required-products-and-components"></a><span data-ttu-id="e9617-142">Instalace požadovaných produktů a součásti</span><span class="sxs-lookup"><span data-stu-id="e9617-142">Install Required Products and Components</span></span>

<span data-ttu-id="e9617-143">Povolit server sestavení pro vytváření řešení, musíte nainstalovat všechny produkty, součásti nebo sestavení, která vyžaduje vaše řešení.</span><span class="sxs-lookup"><span data-stu-id="e9617-143">To enable the build server to build your solutions, you must install any products, components, or assemblies that your solution requires.</span></span> <span data-ttu-id="e9617-144">Než nainstalujete všechny komponenty webové platformy, měli byste nainstalovat Visual Studio 2010 (libovolná verze) na serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-144">Before you install any web platform components, you should install Visual Studio 2010 (any version) on the build server.</span></span> <span data-ttu-id="e9617-145">Tím se zajistí, že jsou k dispozici ve službě sestavení cílové soubory jádra Microsoft Build Engine (MSBuild) a cílové soubory webových publikování kanálu (WPP).</span><span class="sxs-lookup"><span data-stu-id="e9617-145">This ensures that the core Microsoft Build Engine (MSBuild) target files and the Web Publishing Pipeline (WPP) target files are available to the build service.</span></span> <span data-ttu-id="e9617-146">Instalační program sady Visual Studio by měl také nainstalovat nasazení webu, který budete potřebovat, pokud plánujete nasazení webových balíčků jako součást procesu sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-146">The Visual Studio installer should also install Web Deploy, which you'll need if you plan to deploy web packages as part of your build process.</span></span>

<span data-ttu-id="e9617-147">Nejlepší způsob, jak nainstalovat běžné komponenty webové platformy je použít [instalačního programu webové platformy](https://go.microsoft.com/?linkid=9805118).</span><span class="sxs-lookup"><span data-stu-id="e9617-147">The best way to install common web platform components is to use the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span> <span data-ttu-id="e9617-148">Tím se zajistí, že instalujete nejnovější verzi každého produktu, a taky automaticky rozpozná a nainstaluje všechny požadované součásti pro jednotlivé produkty.</span><span class="sxs-lookup"><span data-stu-id="e9617-148">This ensures that you're installing the latest version of each product, and it also automatically detects and installs any prerequisites for each product.</span></span> <span data-ttu-id="e9617-149">V případě třídy [Správce kontaktů](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) řešení, používejte instalačního programu webové platformy nainstalovat tyto produkty a komponenty:</span><span class="sxs-lookup"><span data-stu-id="e9617-149">In the case of the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) solution, you should use the Web Platform Installer to install these products and components:</span></span>

- <span data-ttu-id="e9617-150">**.NET Framework 4.0**.</span><span class="sxs-lookup"><span data-stu-id="e9617-150">**.NET Framework 4.0**.</span></span> <span data-ttu-id="e9617-151">To je potřeba ke spouštění aplikací, které byly vytvořeny v této verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e9617-151">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="e9617-152">**Webové nástroje pro nasazení 2.1 nebo novější**.</span><span class="sxs-lookup"><span data-stu-id="e9617-152">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="e9617-153">Tím se nainstaluje Web Deploy (a její podkladové spustitelný soubor MSDeploy.exe) na serveru.</span><span class="sxs-lookup"><span data-stu-id="e9617-153">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="e9617-154">V rámci tohoto procesu se nainstaluje a spustí služba agenta nasazení webu.</span><span class="sxs-lookup"><span data-stu-id="e9617-154">As part of this process, it installs and starts the Web Deployment Agent Service.</span></span> <span data-ttu-id="e9617-155">Tato služba vám umožní nasadit webových balíčků ze vzdáleného počítače.</span><span class="sxs-lookup"><span data-stu-id="e9617-155">This service lets you deploy web packages from a remote computer.</span></span>
- <span data-ttu-id="e9617-156">**ASP.NET MVC 3**.</span><span class="sxs-lookup"><span data-stu-id="e9617-156">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="e9617-157">Tím se nainstaluje sestavení, je potřeba spouštět aplikace ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="e9617-157">This installs the assemblies you need to run ASP.NET MVC 3 applications.</span></span>

<span data-ttu-id="e9617-158">**Chcete-li nainstalovat požadované produkty a komponenty**</span><span class="sxs-lookup"><span data-stu-id="e9617-158">**To install the required products and components**</span></span>

1. <span data-ttu-id="e9617-159">Install Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="e9617-159">Install Visual Studio 2010.</span></span> <span data-ttu-id="e9617-160">Po zobrazení výzvy vyberte funkce určené k instalaci, měli byste zahrnout:</span><span class="sxs-lookup"><span data-stu-id="e9617-160">When prompted to select features to install, you should include:</span></span>

    1. <span data-ttu-id="e9617-161">Žádné programovací jazyky, které potřebujete ke kompilaci.</span><span class="sxs-lookup"><span data-stu-id="e9617-161">Any programming languages that you need to compile.</span></span>
    2. <span data-ttu-id="e9617-162">Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="e9617-162">Visual Web Developer.</span></span> <span data-ttu-id="e9617-163">Tím se zajistí, že WPP cíle, které jsou přidány do serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-163">This ensures that the WPP targets are added to your build server.</span></span>

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. <span data-ttu-id="e9617-164">Po dokončení instalace sady Visual Studio 2010, stáhněte a nainstalujte [Visual Studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) (Pokud je již není součástí instalačního média).</span><span class="sxs-lookup"><span data-stu-id="e9617-164">When the installation of Visual Studio 2010 is complete, download and install [Visual Studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) (if it's not already included in your installation media).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e9617-165">Visual Studio 2010 Service Pack 1 řeší chybu, která může zabránit vyhledání MSDeploy spustitelný soubor MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e9617-165">Visual Studio 2010 Service Pack 1 resolves a bug that can prevent MSBuild from locating the MSDeploy executable.</span></span>
3. <span data-ttu-id="e9617-166">Stáhnout a spustit [instalačního programu webové platformy](https://go.microsoft.com/?linkid=9805118).</span><span class="sxs-lookup"><span data-stu-id="e9617-166">Download and launch the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
4. <span data-ttu-id="e9617-167">V horní části **3.0 Instalační služby webové platformy** okna, klikněte na tlačítko **produkty**.</span><span class="sxs-lookup"><span data-stu-id="e9617-167">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
5. <span data-ttu-id="e9617-168">Na levé straně okna, v navigačním podokně klikněte na tlačítko **architektury**.</span><span class="sxs-lookup"><span data-stu-id="e9617-168">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
6. <span data-ttu-id="e9617-169">V **rozhraní Microsoft .NET Framework 4** řádek, pokud rozhraní .NET Framework není nainstalovaná, klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="e9617-169">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e9617-170">Možná jste již nainstalovali .NET Framework 4.0 prostřednictvím služby Windows Update.</span><span class="sxs-lookup"><span data-stu-id="e9617-170">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="e9617-171">Pokud už je nainstalován produkt nebo komponenty, instalačního programu webové platformy se označit to tak, že nahradíte **přidat** tlačítko s textem **nainstalováno**.</span><span class="sxs-lookup"><span data-stu-id="e9617-171">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. <span data-ttu-id="e9617-172">V **ASP.NET MVC 3 (Visual Studio 2010)** řádku, klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="e9617-172">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
8. <span data-ttu-id="e9617-173">V navigačním podokně klikněte na tlačítko **Server**.</span><span class="sxs-lookup"><span data-stu-id="e9617-173">In the navigation pane, click **Server**.</span></span>
9. <span data-ttu-id="e9617-174">V **2.1 nástroj Web Deployment** řádku, klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="e9617-174">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="e9617-175">Klikněte na tlačítko **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="e9617-175">Click **Install**.</span></span> <span data-ttu-id="e9617-176">Instalace webové platformy zobrazí seznam produktů&#x2014;spolu s případnými přidružené závislosti&#x2014;k instalaci a zobrazí výzvu k potvrzení licenčních podmínek.</span><span class="sxs-lookup"><span data-stu-id="e9617-176">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>
11. <span data-ttu-id="e9617-177">Přečtěte si licenční podmínky a pokud souhlasíte s podmínkami, klikněte na tlačítko **souhlasím**.</span><span class="sxs-lookup"><span data-stu-id="e9617-177">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="e9617-178">Po dokončení instalace klikněte na tlačítko **Dokončit**a pak zavřete **3.0 Instalační služby webové platformy** okna.</span><span class="sxs-lookup"><span data-stu-id="e9617-178">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

> [!NOTE]
> <span data-ttu-id="e9617-179">Pokud váš proces nasazení obsahuje nástroje, jako je VSDBCMD.exe nebo SQLCMD.exe, budete muset zajistit, aby byly nainstalovány na vašem serveru sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9617-179">If your deployment process includes the use of tools like VSDBCMD.exe or SQLCMD.exe, you'll need to ensure that these are installed on your build server.</span></span> <span data-ttu-id="e9617-180">VSDBCMD.exe je nástroj sady Visual Studio a je obvykle přidána na server, když instalujete Team Foundation Build.</span><span class="sxs-lookup"><span data-stu-id="e9617-180">VSDBCMD.exe is a Visual Studio tool and is typically added to the server when you install Team Foundation Build.</span></span> <span data-ttu-id="e9617-181">SQLCMD.exe je nástroj SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9617-181">SQLCMD.exe is a SQL Server tool.</span></span> <span data-ttu-id="e9617-182">Můžete stáhnout samostatné verze SQLCMD.exe z [Microsoft SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/?linkid=9805134) stránky.</span><span class="sxs-lookup"><span data-stu-id="e9617-182">You can download a stand-alone version of SQLCMD.exe from the [Microsoft SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/?linkid=9805134) page.</span></span>


## <a name="conclusion"></a><span data-ttu-id="e9617-183">Závěr</span><span class="sxs-lookup"><span data-stu-id="e9617-183">Conclusion</span></span>

<span data-ttu-id="e9617-184">V tuto chvíli váš server sestavení připravený začít vytvářet a nasazovat vaše projekty webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="e9617-184">At this point, your build server is ready to start building and deploying your web application projects.</span></span> <span data-ttu-id="e9617-185">Dalším tématu s názvem [vytvoření sestavení definice, že podporuje nasazení](creating-a-build-definition-that-supports-deployment.md), popisuje, jak vytvořit a nakonfigurovat definici sestavení, které řídí, kdy a jak jsou vaše projekty sestavíte a nasadíte.</span><span class="sxs-lookup"><span data-stu-id="e9617-185">The next topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md), describes how to create and configure a build definition to control when and how your projects are built and deployed.</span></span>

## <a name="further-reading"></a><span data-ttu-id="e9617-186">Další čtení</span><span class="sxs-lookup"><span data-stu-id="e9617-186">Further Reading</span></span>

<span data-ttu-id="e9617-187">Další obecné informace o práci s Team Build najdete v tématu [Správa Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9617-187">For more general guidance on working with Team Build, see [Administering Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e9617-188">[Předchozí](adding-content-to-source-control.md)
> [další](creating-a-build-definition-that-supports-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="e9617-188">[Previous](adding-content-to-source-control.md)
[Next](creating-a-build-definition-that-supports-deployment.md)</span></span>