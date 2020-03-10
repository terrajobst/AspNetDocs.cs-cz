---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: Vytvoření a spuštění souboru příkazů nasazení | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak vytvořit soubor příkazů, který vám umožní spustit nasazení pomocí souborů projektu Microsoft Build Engine (MSBuild) v jednom kroku, znovu...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634307"
---
# <a name="creating-and-running-a-deployment-command-file"></a><span data-ttu-id="81062-103">Vytvoření a spuštění souboru příkazů k nasazení</span><span class="sxs-lookup"><span data-stu-id="81062-103">Creating and Running a Deployment Command File</span></span>

<span data-ttu-id="81062-104">od [Jason Novák](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="81062-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="81062-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="81062-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="81062-106">Toto téma popisuje, jak vytvořit soubor příkazů, který vám umožní spustit nasazení pomocí souborů projektu Microsoft Build Engine (MSBuild) jako jeden krok s možností opakování.</span><span class="sxs-lookup"><span data-stu-id="81062-106">This topic describes how to build a command file that will let you run a deployment using Microsoft Build Engine (MSBuild) project files as a single-step, repeatable process.</span></span>

<span data-ttu-id="81062-107">Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého řešení [](the-contact-manager-solution.md) &#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.</span><span class="sxs-lookup"><span data-stu-id="81062-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="81062-108">Metoda nasazení na srdce těchto výukových programů je založena na způsobu sestavení rozděleného projektu popsaných v tématu [Principy procesu sestavení](understanding-the-build-process.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro prostředí.</span><span class="sxs-lookup"><span data-stu-id="81062-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="81062-109">V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.</span><span class="sxs-lookup"><span data-stu-id="81062-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="process-overview"></a><span data-ttu-id="81062-110">Přehled procesu</span><span class="sxs-lookup"><span data-stu-id="81062-110">Process Overview</span></span>

<span data-ttu-id="81062-111">V tomto tématu se dozvíte, jak vytvořit a spustit soubor příkazů, který pomocí těchto souborů projektu provede opakované nasazení do cílového prostředí.</span><span class="sxs-lookup"><span data-stu-id="81062-111">In this topic, you'll learn how to create and run a command file that uses these project files to perform a repeatable deployment to your target environment.</span></span> <span data-ttu-id="81062-112">V podstatě musí soubor příkazů jednoduše obsahovat příkaz MSBuild, který:</span><span class="sxs-lookup"><span data-stu-id="81062-112">Essentially, the command file simply needs to contain an MSBuild command that:</span></span>

- <span data-ttu-id="81062-113">Instruuje nástroj MSBuild, aby spustil soubor nezávislá *Publish. proj* .</span><span class="sxs-lookup"><span data-stu-id="81062-113">Tells MSBuild to execute the environment-agnostic *Publish.proj* file.</span></span>
- <span data-ttu-id="81062-114">Informuje soubor *Publish. proj* , který obsahuje nastavení projektu konkrétního prostředí a kde se má najít.</span><span class="sxs-lookup"><span data-stu-id="81062-114">Tells the *Publish.proj* file which file contains the environment-specific project settings and where to find it.</span></span>

## <a name="create-an-msbuild-command"></a><span data-ttu-id="81062-115">Vytvoření příkazu MSBuild</span><span class="sxs-lookup"><span data-stu-id="81062-115">Create an MSBuild Command</span></span>

<span data-ttu-id="81062-116">Jak je popsáno v tématu [Principy procesu sestavení](understanding-the-build-process.md), soubor&#x2014;projektu specifický pro prostředí, například *ENV-dev. proj*&#x2014;, je navržen pro import do souboru Publish-nezávislá *Publish. proj* v čase sestavení.</span><span class="sxs-lookup"><span data-stu-id="81062-116">As described in [Understanding the Build Process](understanding-the-build-process.md), the environment-specific project file&#x2014;for example, *Env-Dev.proj*&#x2014;is designed to be imported into the environment-agnostic *Publish.proj* file at build time.</span></span> <span data-ttu-id="81062-117">Společně tyto dva soubory poskytují kompletní sadu instrukcí, které nástroj MSBuild sdělí, jak sestavit a nasadit vaše řešení.</span><span class="sxs-lookup"><span data-stu-id="81062-117">Together, these two files provide a complete set of instructions that tell MSBuild how to build and deploy your solution.</span></span>

<span data-ttu-id="81062-118">Soubor *Publish. proj* používá prvek **Import** pro import souboru projektu specifického pro prostředí.</span><span class="sxs-lookup"><span data-stu-id="81062-118">The *Publish.proj* file uses an **Import** element to import the environment-specific project file.</span></span>

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

<span data-ttu-id="81062-119">V takovém případě, když k sestavení a nasazení řešení Contact Manager použijete nástroj MSBuild. exe, musíte:</span><span class="sxs-lookup"><span data-stu-id="81062-119">As such, when you use MSBuild.exe to build and deploy the Contact Manager solution, you need to:</span></span>

- <span data-ttu-id="81062-120">Spusťte nástroj MSBuild. exe v souboru *Publish. proj* .</span><span class="sxs-lookup"><span data-stu-id="81062-120">Run MSBuild.exe on the *Publish.proj* file.</span></span>
- <span data-ttu-id="81062-121">Zadáním parametru příkazového řádku s názvem **TargetEnvPropsFile**zadejte umístění souboru projektu specifického pro prostředí.</span><span class="sxs-lookup"><span data-stu-id="81062-121">Specify the location of the environment-specific project file by supplying a command-line parameter named **TargetEnvPropsFile**.</span></span>

<span data-ttu-id="81062-122">Chcete-li to provést, váš příkaz MSBuild by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="81062-122">To do this, your MSBuild command should resemble this:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

<span data-ttu-id="81062-123">Tady je jednoduchý krok pro přechod k opakovanému nasazení v jednom kroku.</span><span class="sxs-lookup"><span data-stu-id="81062-123">From here, it's a simple step to move to a repeatable, single-step deployment.</span></span> <span data-ttu-id="81062-124">Vše, co potřebujete udělat, je přidání příkazu MSBuild do souboru. cmd.</span><span class="sxs-lookup"><span data-stu-id="81062-124">All you need to do is to add your MSBuild command to a .cmd file.</span></span> <span data-ttu-id="81062-125">V řešení Správce kontaktů obsahuje složka pro publikování soubor s názvem *Publish-dev. cmd* , který to přesně dělá.</span><span class="sxs-lookup"><span data-stu-id="81062-125">In the Contact Manager solution, the Publish folder includes a file named *Publish-Dev.cmd* that does exactly this.</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="81062-126">Přepínač **/FL** instruuje nástroj MSBuild, aby vytvořil soubor protokolu s názvem *MSBuild. log* v pracovním adresáři, ve kterém byl spuštěn nástroj MSBuild. exe.</span><span class="sxs-lookup"><span data-stu-id="81062-126">The **/fl** switch instructs MSBuild to create a log file named *msbuild.log* in the working directory in which MSBuild.exe was invoked.</span></span>

<span data-ttu-id="81062-127">K nasazení nebo opětovnému nasazení řešení Contact Manager stačí, když spustíte soubor *Publish-dev. cmd* .</span><span class="sxs-lookup"><span data-stu-id="81062-127">To deploy or redeploy the Contact Manager solution, all you need to do is run the *Publish-Dev.cmd* file.</span></span> <span data-ttu-id="81062-128">Když soubor spustíte, MSBuild provede:</span><span class="sxs-lookup"><span data-stu-id="81062-128">When you run the file, MSBuild will:</span></span>

- <span data-ttu-id="81062-129">Sestavujte všechny projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="81062-129">Build all the projects in the solution.</span></span>
- <span data-ttu-id="81062-130">Vygenerujte nasazené webové balíčky pro projekty webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="81062-130">Generate deployable web packages for the web application projects.</span></span>
- <span data-ttu-id="81062-131">Vygenerujte soubory. dbschema a. DeployManifest pro databázové projekty.</span><span class="sxs-lookup"><span data-stu-id="81062-131">Generate .dbschema and .deploymanifest files for the database projects.</span></span>
- <span data-ttu-id="81062-132">Nasaďte webové balíčky na webový server.</span><span class="sxs-lookup"><span data-stu-id="81062-132">Deploy the web packages to the web server.</span></span>
- <span data-ttu-id="81062-133">Nasaďte databázi na databázový server.</span><span class="sxs-lookup"><span data-stu-id="81062-133">Deploy the database to the database server.</span></span>

## <a name="run-the-deployment"></a><span data-ttu-id="81062-134">Spustit nasazení</span><span class="sxs-lookup"><span data-stu-id="81062-134">Run the Deployment</span></span>

<span data-ttu-id="81062-135">Když jste vytvořili soubor příkazů pro cílové prostředí, měli byste být schopni dokončit celé nasazení pouhým spuštěním souboru.</span><span class="sxs-lookup"><span data-stu-id="81062-135">When you've created a command file for your target environment, you should be able to complete the entire deployment by simply running the file.</span></span>

<span data-ttu-id="81062-136">**Nasazení řešení Contact Manageru do testovacího prostředí**</span><span class="sxs-lookup"><span data-stu-id="81062-136">**To deploy the Contact Manager solution to your test environment**</span></span>

1. <span data-ttu-id="81062-137">Na pracovní stanici pro vývojáře otevřete Průzkumníka Windows a přejděte do umístění souboru *Publish-dev. cmd* .</span><span class="sxs-lookup"><span data-stu-id="81062-137">On your developer workstation, open Windows Explorer, and then browse to the location of the *Publish-Dev.cmd* file.</span></span>
2. <span data-ttu-id="81062-138">Dvakrát klikněte na soubor a spusťte ho.</span><span class="sxs-lookup"><span data-stu-id="81062-138">Double-click the file to run it.</span></span>
3. <span data-ttu-id="81062-139">Pokud se zobrazí dialogové okno **otevřít soubor – upozornění zabezpečení** , klikněte na **Spustit**.</span><span class="sxs-lookup"><span data-stu-id="81062-139">If an **Open File – Security Warning** dialog box appears, click **Run**.</span></span>
4. <span data-ttu-id="81062-140">Pokud jsou nastavení konfigurace a testovací servery správně nastaveny, okno příkazového řádku zobrazí zprávu o **úspěšném sestavení** po dokončení zpracování souborů projektu v nástroji MSBuild.</span><span class="sxs-lookup"><span data-stu-id="81062-140">If your configuration settings and test servers are set up correctly, the Command Prompt window will show a **Build succeeded** message when MSBuild has finished processing the project files.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. <span data-ttu-id="81062-141">Pokud toto řešení nasadíte poprvé do tohoto prostředí, budete muset přidat účet počítače testovacího webového serveru do role databáze **\_datawrite** a **DB\_DataReader** v databázi **ContactManager** .</span><span class="sxs-lookup"><span data-stu-id="81062-141">If this is the first time you've deployed the solution to this environment, you'll need to add the test web server machine account to the **db\_datawriter** and **db\_datareader** roles on the **ContactManager** database.</span></span> <span data-ttu-id="81062-142">Tento postup je popsaný v tématu [Konfigurace databázového serveru pro publikování nasazení webu](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="81062-142">This procedure is described in [Configure a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="81062-143">Tato oprávnění je potřeba přiřadit jenom při vytváření databáze.</span><span class="sxs-lookup"><span data-stu-id="81062-143">You only need to assign these permissions when you create the database.</span></span> <span data-ttu-id="81062-144">Ve výchozím nastavení vytvoří proces sestavení databázi znovu při každém nasazení&#x2014;, porovná stávající databázi s nejnovějším schématem a provede pouze změny.</span><span class="sxs-lookup"><span data-stu-id="81062-144">By default, the build process will not recreate the database on every deployment&#x2014;instead, it will compare the existing database to the latest schema and make only the changes required.</span></span> <span data-ttu-id="81062-145">V důsledku toho byste měli tyto databázové role namapovat jenom při prvním nasazení řešení.</span><span class="sxs-lookup"><span data-stu-id="81062-145">As a result, you should only need to map these database roles the first time you deploy the solution.</span></span>
6. <span data-ttu-id="81062-146">Spusťte Internet Explorer a přejděte na adresu URL aplikace Správce kontaktů (například `http://testweb1:85/ContactManager/`).</span><span class="sxs-lookup"><span data-stu-id="81062-146">Open Internet Explorer and browse to the URL of the Contact Manager application (for example, `http://testweb1:85/ContactManager/`).</span></span>
7. <span data-ttu-id="81062-147">Ověřte, že aplikace funguje podle očekávání a že je možné přidat kontakty.</span><span class="sxs-lookup"><span data-stu-id="81062-147">Verify that the application works as expected and you're able to add contacts.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="81062-148">Závěr</span><span class="sxs-lookup"><span data-stu-id="81062-148">Conclusion</span></span>

<span data-ttu-id="81062-149">Vytvoření souboru příkazů obsahujícího pokyny MSBuild vám poskytne rychlý a snadný způsob, jak sestavit a nasadit řešení pro více projektů do konkrétního cílového prostředí.</span><span class="sxs-lookup"><span data-stu-id="81062-149">Creating a command file containing your MSBuild instructions provides you with a quick and easy way of building and deploying a multi-project solution to a specific destination environment.</span></span> <span data-ttu-id="81062-150">Pokud potřebujete řešení opakovaně nasadit do více cílových prostředí, můžete vytvořit více souborů příkazů.</span><span class="sxs-lookup"><span data-stu-id="81062-150">If you need to repeatedly deploy your solution to multiple destination environments, you can create multiple command files.</span></span> <span data-ttu-id="81062-151">V každém souboru příkazů příkaz MSBuild sestaví stejný soubor univerzálního projektu, ale určí jiný projekt specifický pro prostředí.</span><span class="sxs-lookup"><span data-stu-id="81062-151">In each command file, the MSBuild command will build the same universal project file, but it will specify a different environment-specific project file.</span></span> <span data-ttu-id="81062-152">Například soubor příkazů pro publikování do vývojového nebo testovacího prostředí může obsahovat tento příkaz MSBuild:</span><span class="sxs-lookup"><span data-stu-id="81062-152">For example, a command file to publish to a developer or test environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

<span data-ttu-id="81062-153">Soubor příkazů pro publikování do přípravného prostředí může obsahovat tento příkaz MSBuild:</span><span class="sxs-lookup"><span data-stu-id="81062-153">A command file to publish to a staging environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> <span data-ttu-id="81062-154">Pokyny k přizpůsobení souborů projektu specifických pro prostředí pro vlastní serverová prostředí najdete v tématu [Konfigurace vlastností nasazení pro cílové prostředí](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span><span class="sxs-lookup"><span data-stu-id="81062-154">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>

<span data-ttu-id="81062-155">Proces sestavení můžete také přizpůsobit pro každé prostředí přepsáním vlastností nebo nastavením různých dalších přepínačů v příkazu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="81062-155">You can also customize the build process for each environment by overriding properties or setting various other switches in your MSBuild command.</span></span> <span data-ttu-id="81062-156">Další informace najdete v tématu [Reference k příkazovému řádku MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).</span><span class="sxs-lookup"><span data-stu-id="81062-156">For more information, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="81062-157">[Předchozí](deploying-database-projects.md)
> [Další](manually-installing-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="81062-157">[Previous](deploying-database-projects.md)
[Next](manually-installing-web-packages.md)</span></span>
