---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: Konfigurace oprávnění pro tým nasazení sestavení | Dokumentace Microsoftu
author: jrjlee
description: Toto téma popisuje, jak nakonfigurovat oprávnění, které umožňují sestavení serveru nasazení obsahu do webové servery a databázové servery jako součást automatizovaného b...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 0142be694a4e7d601625022f6fbfe39971823d03
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076306"
---
<a name="configuring-permissions-for-team-build-deployment"></a><span data-ttu-id="78cc1-103">Konfigurace oprávnění pro nasazení týmového sestavení</span><span class="sxs-lookup"><span data-stu-id="78cc1-103">Configuring Permissions for Team Build Deployment</span></span>
====================
<span data-ttu-id="78cc1-104">podle [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="78cc1-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="78cc1-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="78cc1-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="78cc1-106">Toto téma popisuje, jak nakonfigurovat oprávnění, které umožňují sestavení serveru nasazení obsahu do webové servery a databázové servery jako součást automatizovaného procesu sestavení.</span><span class="sxs-lookup"><span data-stu-id="78cc1-106">This topic describes how to configure permissions to enable your build server to deploy content to web servers and database servers as part of an automated build process.</span></span>


<span data-ttu-id="78cc1-107">Toto téma je součástí série kurzů podle požadavků na nasazení enterprise fiktivní společnosti s názvem společnosti Fabrikam, Inc. V této sérii kurzů používá ukázkové řešení&#x2014; [řešení Správce kontaktů](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;představující webovou aplikaci s realistické úroveň složitosti, včetně aplikace ASP.NET MVC 3, komunikace Windows Služba Foundation (WCF) a databázový projekt.</span><span class="sxs-lookup"><span data-stu-id="78cc1-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="78cc1-108">Metody nasazení v srdci těchto kurzů je založen na rozdělení přístupu soubor projektu je popsáno v [vysvětlení souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve které je řízena procesem sestavení dva soubory projektu&#x2014;jeden obsahující pokyny, které platí pro všechny cílové prostředí a jeden obsahuje nastavení pro konkrétní prostředí sestavení a nasazení pro sestavení.</span><span class="sxs-lookup"><span data-stu-id="78cc1-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="78cc1-109">V okamžiku sestavení souboru projektu specifických pro prostředí se sloučí do souboru projektu bez ohledu na prostředí a vytvoří kompletní sadu pokynů sestavení.</span><span class="sxs-lookup"><span data-stu-id="78cc1-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="78cc1-110">Přehled úloh</span><span class="sxs-lookup"><span data-stu-id="78cc1-110">Task Overview</span></span>

<span data-ttu-id="78cc1-111">Při instalaci služby Team Foundation Server (TFS) 2010 sestavení, zadejte identitu, se kterým se má službu spustit.</span><span class="sxs-lookup"><span data-stu-id="78cc1-111">When you install the Team Foundation Server (TFS) 2010 build service, you specify the identity with which you want the service to run.</span></span> <span data-ttu-id="78cc1-112">Ve výchozím nastavení je to účet síťové služby.</span><span class="sxs-lookup"><span data-stu-id="78cc1-112">By default, this is the Network Service account.</span></span> <span data-ttu-id="78cc1-113">Alternativně můžete nakonfigurovat službu sestavení ke spuštění pomocí účtu domény.</span><span class="sxs-lookup"><span data-stu-id="78cc1-113">Alternatively, you can configure the build service to run using a domain account.</span></span>

<span data-ttu-id="78cc1-114">Úkoly nasazení, které vyžadují ověřování Windows a plánujete automatizovat pomocí Team Build, bude spuštěna s použitím identity služby sestavení.</span><span class="sxs-lookup"><span data-stu-id="78cc1-114">Any deployment tasks that require Windows authentication, and that you plan to automate using Team Build, will run using the build service identity.</span></span> <span data-ttu-id="78cc1-115">V důsledku toho budete muset udělit identitu služby sestavení jakékoli požadovaná oprávnění pro vaše webové servery a databázové servery.</span><span class="sxs-lookup"><span data-stu-id="78cc1-115">As such, you'll need to grant the build service identity any required permissions on your web servers and your database servers.</span></span>

> [!NOTE]
> <span data-ttu-id="78cc1-116">Účet Network Service používá účet počítače pro ověření do jiných počítačů.</span><span class="sxs-lookup"><span data-stu-id="78cc1-116">The Network Service account uses the machine account to authenticate to other computers.</span></span> <span data-ttu-id="78cc1-117">Účty počítače mít podobu *[název domény]\[název počítače]* **$**&#x2014;například **FABRIKAM\TFSBUILD$**.</span><span class="sxs-lookup"><span data-stu-id="78cc1-117">Machine accounts take the form \*[domain name]\[machine name]\***$**&#x2014;for example, **FABRIKAM\TFSBUILD$**.</span></span> <span data-ttu-id="78cc1-118">V důsledku toho pokud je sestavovací služba spuštěná, používat identitu síťové služby, byste měli udělit libovolné požadovaná oprávnění pro identitu účtu počítače pro váš server sestavení.</span><span class="sxs-lookup"><span data-stu-id="78cc1-118">As such, if your build service runs using the Network Service identity, you should grant any required permissions to the machine account identity for your build server.</span></span>


## <a name="configuring-web-server-permissions"></a><span data-ttu-id="78cc1-119">Konfigurace oprávnění webového serveru</span><span class="sxs-lookup"><span data-stu-id="78cc1-119">Configuring Web Server Permissions</span></span>

<span data-ttu-id="78cc1-120">Jak je popsáno v [výběr právo přístupu k nasazení webu](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), existují dva hlavní přístupy, které můžete použít, pokud chcete nasadit webových balíčků na vzdáleném webovém serveru:</span><span class="sxs-lookup"><span data-stu-id="78cc1-120">As described in [Choosing the Right Approach to Web Deployment](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), there are two main approaches you can use if you want to deploy web packages to a remote web server:</span></span>

- <span data-ttu-id="78cc1-121">Nasadit aplikaci ze vzdáleného umístění pomocí cílení *webová služba agenta nasazení* (označované také jako vzdálený agent) na cílovém serveru.</span><span class="sxs-lookup"><span data-stu-id="78cc1-121">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the remote agent) on the destination server.</span></span>
- <span data-ttu-id="78cc1-122">Nasadit aplikaci ze vzdáleného umístění pomocí cílení *Internetová informační služba* (*služby IIS) obslužné rutiny webu nasadit* na cílovém serveru.</span><span class="sxs-lookup"><span data-stu-id="78cc1-122">Deploy the application from a remote location by targeting the *Internet Information Services* (*IIS) Web Deploy Handler* on the destination server.</span></span>

<span data-ttu-id="78cc1-123">Vzdálený agent v tomto případě má dva klíče omezení:</span><span class="sxs-lookup"><span data-stu-id="78cc1-123">The remote agent has two key limitations in this case:</span></span>

- <span data-ttu-id="78cc1-124">Vzdálený agent podporuje pouze ověřování NTLM.</span><span class="sxs-lookup"><span data-stu-id="78cc1-124">The remote agent supports only NTLM authentication.</span></span> <span data-ttu-id="78cc1-125">Jinými slovy, nasazení musí používat identitu služby sestavení&#x2014;nelze zosobnit jiného účtu.</span><span class="sxs-lookup"><span data-stu-id="78cc1-125">In other words, the deployment must use the build service identity&#x2014;you can't impersonate another account.</span></span>
- <span data-ttu-id="78cc1-126">Použití vzdáleného agenta, musí být účet, který nasazení provádí správce na cílovém serveru.</span><span class="sxs-lookup"><span data-stu-id="78cc1-126">To use the remote agent, the account that performs the deployment must be an administrator on the target server.</span></span>

<span data-ttu-id="78cc1-127">Společně tyto dvě omezení Ujistěte se, vzdálený agent přístup nežádoucí pro automatické nasazení Team Build.</span><span class="sxs-lookup"><span data-stu-id="78cc1-127">Together, these two limitations make the remote agent approach undesirable for an automated Team Build deployment.</span></span> <span data-ttu-id="78cc1-128">Chcete-li tuto metodu použijte, je třeba službu sestavení účtu správce na všechny cílové webové servery.</span><span class="sxs-lookup"><span data-stu-id="78cc1-128">To use this approach, you'd need to make the build service account an administrator on any target web servers.</span></span>

<span data-ttu-id="78cc1-129">Naproti tomu obslužná rutina nasazení webového přístupu nabízí různé výhody:</span><span class="sxs-lookup"><span data-stu-id="78cc1-129">In contrast, the Web Deploy Handler approach offers various advantages:</span></span>

- <span data-ttu-id="78cc1-130">Obslužné rutiny nasazení webu podporuje základní ověřování přes protokol HTTPS, který umožňuje předání přihlašovacích údajů účtu alternativní nástroj nasazení webu služby IIS (Web Deploy).</span><span class="sxs-lookup"><span data-stu-id="78cc1-130">The Web Deploy Handler supports basic authentication over HTTPS, which allows you to pass the credentials of an alternative account to the IIS Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="78cc1-131">Můžete nakonfigurovat cílové webové servery umožňuje uživatelům bez oprávnění správce pro nasazení obsahu pro konkrétní weby služby IIS pomocí obslužné rutiny nasazení webu.</span><span class="sxs-lookup"><span data-stu-id="78cc1-131">You can configure target web servers to allow non-administrator users to deploy content to specific IIS websites using the Web Deploy Handler.</span></span>

<span data-ttu-id="78cc1-132">V důsledku toho je vhodnější jasně cílit obslužné rutiny nasazení webu při automatizaci nasazení webového balíčku z nástroje týmové sestavení.</span><span class="sxs-lookup"><span data-stu-id="78cc1-132">As a result, it's clearly preferable to target the Web Deploy Handler when you automate web package deployment from Team Build.</span></span> <span data-ttu-id="78cc1-133">Toto je doporučený postup:</span><span class="sxs-lookup"><span data-stu-id="78cc1-133">This is the recommended process:</span></span>

1. <span data-ttu-id="78cc1-134">Vytvořte účet domény s nízkým oprávněním, který chcete použít pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="78cc1-134">Create a low-privileged domain account to use for the deployment.</span></span>
2. <span data-ttu-id="78cc1-135">Nakonfigurujte obslužné rutiny nasazení webu a účtu udělit požadovaná oprávnění pro nasazení obsahu pro konkrétní web služby IIS, jak je popsáno v [konfigurace webového serveru pro nasazení publikování na webu (nasazení obslužná rutina webových)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span><span class="sxs-lookup"><span data-stu-id="78cc1-135">Configure the Web Deploy Handler and grant the account the required permissions to deploy content to a specific IIS website, as described in [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span>
3. <span data-ttu-id="78cc1-136">Vyvolání Web Deploy a cílové obslužné rutiny nasazení webu, použití základního ověřování a poskytnutí přihlašovacích údajů účtu domény právě vytvořili, a provést nasazení.</span><span class="sxs-lookup"><span data-stu-id="78cc1-136">Invoke Web Deploy and target the Web Deploy Handler, using basic authentication and supplying the credentials of the domain account you created, to perform the deployment.</span></span>

<span data-ttu-id="78cc1-137">V [Správce kontaktů](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) ukázkové řešení, určete typ ověřování (základní nebo NTLM), přihlašovací údaje pro nasazení webu a adresu koncového bodu (vzdálený agent nebo obslužné rutiny nasazení webu) v souboru projektu pro konkrétní prostředí.</span><span class="sxs-lookup"><span data-stu-id="78cc1-137">In the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, you specify the authentication type (basic or NTLM), the Web Deploy credentials, and the endpoint address (remote agent or Web Deploy Handler) in the environment-specific project file.</span></span> <span data-ttu-id="78cc1-138">Tyto hodnoty slouží k formulování a spusťte příkaz Webdeploy při spuštění souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="78cc1-138">These values are used to formulate and run a Web Deploy command when the project file is executed.</span></span> <span data-ttu-id="78cc1-139">Další informace najdete v tématu [nasazení webových balíčků](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span><span class="sxs-lookup"><span data-stu-id="78cc1-139">For more information, see [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

<span data-ttu-id="78cc1-140">Další informace o konfiguraci webové nasazení obslužnou rutinu, včetně postupu konfigurace oprávnění, najdete v části [konfigurace webového serveru pro nasazení publikování na webu (nasazení obslužná rutina webových)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span><span class="sxs-lookup"><span data-stu-id="78cc1-140">For more information on configuring the Web Deploy Handler, including how to configure permissions, see [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="78cc1-141">Další informace o konfiguraci vzdáleného agenta najdete v tématu [konfigurace webového serveru pro nasazení publikování na webu (vzdálený Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span><span class="sxs-lookup"><span data-stu-id="78cc1-141">For more information on configuring the remote agent, see [Configuring a Web Server for Web Deploy Publishing (Remote Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span>

## <a name="configuring-database-server-permissions"></a><span data-ttu-id="78cc1-142">Konfigurace databáze serveru oprávnění</span><span class="sxs-lookup"><span data-stu-id="78cc1-142">Configuring Database Server Permissions</span></span>

<span data-ttu-id="78cc1-143">Nasazení databáze na SQL Server, musíte mít:</span><span class="sxs-lookup"><span data-stu-id="78cc1-143">To deploy a database to SQL Server, you must:</span></span>

- <span data-ttu-id="78cc1-144">Vytvořte přihlašovací údaje pro nasazení účtu v instanci systému SQL Server.</span><span class="sxs-lookup"><span data-stu-id="78cc1-144">Create a login for the deploying account on the SQL Server instance.</span></span>
- <span data-ttu-id="78cc1-145">Udělit přihlášení **DBCreator** oprávnění v instanci systému SQL Server.</span><span class="sxs-lookup"><span data-stu-id="78cc1-145">Grant the login **DBCreator** permissions on the SQL Server instance.</span></span>
- <span data-ttu-id="78cc1-146">Po počátečním nasazení přidat přihlášení **db\_vlastníka** role na cílové databázi.</span><span class="sxs-lookup"><span data-stu-id="78cc1-146">After the initial deployment, add the login to the **db\_owner** role on the target database.</span></span> <span data-ttu-id="78cc1-147">To je povinné, protože na další nasazení, můžete se úprava existující databázi místo vytvoření nové databáze.</span><span class="sxs-lookup"><span data-stu-id="78cc1-147">This is required because on subsequent deployments, you're modifying an existing database rather than creating a new database.</span></span>

<span data-ttu-id="78cc1-148">Můžete se ověřit do instance SQL serveru pomocí ověřování protokolem NTLM nebo ověřování serveru SQL Server:</span><span class="sxs-lookup"><span data-stu-id="78cc1-148">You can authenticate to a SQL Server instance using either NTLM authentication or SQL Server authentication:</span></span>

- <span data-ttu-id="78cc1-149">Pokud používáte ověřování protokolem NTLM, budete muset udělit oprávnění k účtu sestavovací služby je popsáno výše.</span><span class="sxs-lookup"><span data-stu-id="78cc1-149">If you use NTLM authentication, you need to grant the permissions described above to the build service account.</span></span>
- <span data-ttu-id="78cc1-150">Pokud používáte ověřování SQL serveru, musíte udělit oprávnění je popsáno výše pro účet systému SQL Server.</span><span class="sxs-lookup"><span data-stu-id="78cc1-150">If you use SQL Server authentication, you need to grant the permissions described above to the SQL Server account.</span></span> <span data-ttu-id="78cc1-151">Také musíte zahrnout připojovací řetězec, který používáte k nasazení databáze SQL serveru uživatelské jméno a heslo.</span><span class="sxs-lookup"><span data-stu-id="78cc1-151">You also need to include the SQL Server user name and password in the connection string you use to deploy the database.</span></span>

<span data-ttu-id="78cc1-152">Podrobné informace o tom, jak nakonfigurovat oprávnění pro nasazení databáze, najdete v části [konfigurace databázového serveru pro publikování nasazení na webu](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="78cc1-152">For step-by-step details on how to configure permissions for database deployment, see [Configuring a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

## <a name="conclusion"></a><span data-ttu-id="78cc1-153">Závěr</span><span class="sxs-lookup"><span data-stu-id="78cc1-153">Conclusion</span></span>

<span data-ttu-id="78cc1-154">V tomto okamžiku byste měli rozumět oprávnění požadovaná spolu s open, možnosti ověřování při automatizaci nasazení webové aplikace a databáze z nástroje týmové sestavení.</span><span class="sxs-lookup"><span data-stu-id="78cc1-154">At this point, you should understand the permissions required, together with the authentication options open to you, when you automate web application and database deployments from Team Build.</span></span> <span data-ttu-id="78cc1-155">Také by měl být schopni implementovat potřebná oprávnění na webové servery služby IIS a servery databázového serveru SQL Server.</span><span class="sxs-lookup"><span data-stu-id="78cc1-155">You should also be able to implement the necessary permissions on IIS web servers and SQL Server database servers.</span></span>

## <a name="further-reading"></a><span data-ttu-id="78cc1-156">Další čtení</span><span class="sxs-lookup"><span data-stu-id="78cc1-156">Further Reading</span></span>

<span data-ttu-id="78cc1-157">Další informace o konfiguraci prostředí Windows serveru pro podporu vzdáleného nasazení najdete v tématu [konfigurace serveru prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="78cc1-157">For more information on configuring Windows server environments to support remote deployment, see [Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="78cc1-158">Předchozí</span><span class="sxs-lookup"><span data-stu-id="78cc1-158">Previous</span></span>](deploying-a-specific-build.md)