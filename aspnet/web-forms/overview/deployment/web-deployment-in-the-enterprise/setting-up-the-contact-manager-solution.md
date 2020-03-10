---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Nastavení řešení Contact Manager | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak stáhnout a nakonfigurovat řešení Správce kontaktů, aby se spouštělo místně na pracovní stanici pro vývojáře.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629855"
---
# <a name="setting-up-the-contact-manager-solution"></a><span data-ttu-id="49952-103">Nastavení řešení správce kontaktů</span><span class="sxs-lookup"><span data-stu-id="49952-103">Setting Up the Contact Manager Solution</span></span>

<span data-ttu-id="49952-104">od [Jason Novák](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="49952-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="49952-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="49952-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="49952-106">Toto téma popisuje, jak stáhnout a nakonfigurovat řešení Správce kontaktů, aby se spouštělo místně na pracovní stanici pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="49952-106">This topic describes how to download and configure the Contact Manager solution to run locally on a developer workstation.</span></span>

## <a name="system-requirements"></a><span data-ttu-id="49952-107">Systémové požadavky</span><span class="sxs-lookup"><span data-stu-id="49952-107">System Requirements</span></span>

<span data-ttu-id="49952-108">Pokud chcete řešení Správce kontaktů spustit místně a provést další úkoly popsané v tomto kurzu, budete muset tento software nainstalovat na pracovní stanici pro vývojáře:</span><span class="sxs-lookup"><span data-stu-id="49952-108">To run the Contact Manager solution locally and to perform the other tasks described in this tutorial, you'll need to install this software on your developer workstation:</span></span>

- <span data-ttu-id="49952-109">Visual Studio 2010 Service Pack 1, Premium nebo Ultimate Edition</span><span class="sxs-lookup"><span data-stu-id="49952-109">Visual Studio 2010 Service Pack 1, Premium or Ultimate Edition</span></span>
- <span data-ttu-id="49952-110">Internetová informační služba (IIS) 7,5 Express</span><span class="sxs-lookup"><span data-stu-id="49952-110">Internet Information Services (IIS) 7.5 Express</span></span>
- <span data-ttu-id="49952-111">SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="49952-111">SQL Server Express 2008 R2</span></span>
- <span data-ttu-id="49952-112">Nástroj pro nasazení webu služby IIS (Nasazení webu) 2,1 nebo novější</span><span class="sxs-lookup"><span data-stu-id="49952-112">IIS Web Deployment Tool (Web Deploy) 2.1 or later</span></span>
- <span data-ttu-id="49952-113">ASP.NET 4.0</span><span class="sxs-lookup"><span data-stu-id="49952-113">ASP.NET 4.0</span></span>
- <span data-ttu-id="49952-114">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="49952-114">ASP.NET MVC 3</span></span>
- <span data-ttu-id="49952-115">.NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="49952-115">.NET Framework 4</span></span>
- <span data-ttu-id="49952-116">.NET Framework 3.5 SP1</span><span class="sxs-lookup"><span data-stu-id="49952-116">.NET Framework 3.5 SP1</span></span>

<span data-ttu-id="49952-117">S výjimkou sady Visual Studio 2010 můžete stáhnout a nainstalovat nejnovější verze všech těchto produktů a součástí pomocí [instalačního programu webové platformy](https://go.microsoft.com/?linkid=9805118).</span><span class="sxs-lookup"><span data-stu-id="49952-117">With the exception of Visual Studio 2010, you can download and install the latest versions of all of these products and components through the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

## <a name="download-and-extract-the-solution"></a><span data-ttu-id="49952-118">Stažení a extrakce řešení</span><span class="sxs-lookup"><span data-stu-id="49952-118">Download and Extract the Solution</span></span>

<span data-ttu-id="49952-119">Ukázkovou aplikaci Správce kontaktů si můžete stáhnout [z Galerie kódu](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="49952-119">You can download the Contact Manager sample application from the MSDN Code Gallery [here](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).</span></span>

## <a name="configure-and-run-the-solution"></a><span data-ttu-id="49952-120">Konfigurace a spuštění řešení</span><span class="sxs-lookup"><span data-stu-id="49952-120">Configure and Run the Solution</span></span>

<span data-ttu-id="49952-121">Pokud chcete nakonfigurovat a spustit řešení Contact Manageru na místním počítači, musíte provést tyto kroky vysoké úrovně:</span><span class="sxs-lookup"><span data-stu-id="49952-121">To configure and run the Contact Manager solution on your local machine, you'll need to perform these high-level steps:</span></span>

1. <span data-ttu-id="49952-122">Pokud ho ještě nemáte, vytvořte místní databázi ASP.NET aplikačních služeb s povolenými funkcemi členství a správy rolí.</span><span class="sxs-lookup"><span data-stu-id="49952-122">If you don't have one already, create a local ASP.NET application services database with the membership and role management features enabled.</span></span>
2. <span data-ttu-id="49952-123">Upravte připojovací řetězce v souborech *Web. config* tak, aby odkazovaly na místní instanci SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="49952-123">Edit connection strings in the *web.config* files to point to your local SQL Server Express instance.</span></span>
3. <span data-ttu-id="49952-124">Spusťte řešení ze sady Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="49952-124">Run the solution from Visual Studio 2010.</span></span>

<span data-ttu-id="49952-125">Zbývající část této části poskytuje další informace o tom, jak provést každou z těchto úloh.</span><span class="sxs-lookup"><span data-stu-id="49952-125">The remainder of this section provides more guidance on how to complete each of these tasks.</span></span>

<span data-ttu-id="49952-126">**Vytvoření databáze služby Application Services**</span><span class="sxs-lookup"><span data-stu-id="49952-126">**To create the application services database**</span></span>

1. <span data-ttu-id="49952-127">Otevřete příkazový řádek sady Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="49952-127">Open a Visual Studio 2010 command prompt.</span></span> <span data-ttu-id="49952-128">Provedete to tak, že v nabídce **Start** přejdete na položku **všechny programy**, kliknete na možnost **Microsoft Visual Studio 2010**, kliknete na položku **Visual Studio Tools**a potom kliknete na **příkaz Visual Studio Command Prompt (2010)** .</span><span class="sxs-lookup"><span data-stu-id="49952-128">To do this, on the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, click **Visual Studio Tools**, and then click **Visual Studio Command Prompt (2010)**.</span></span>
2. <span data-ttu-id="49952-129">Na příkazovém řádku zadejte tento příkaz a stiskněte klávesu ENTER:</span><span class="sxs-lookup"><span data-stu-id="49952-129">At the command prompt, type this command, and then press Enter:</span></span>

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. <span data-ttu-id="49952-130">Pro zadání připojovacího řetězce pro databázový server použijte přepínač **– C** .</span><span class="sxs-lookup"><span data-stu-id="49952-130">Use the **–C** switch to specify the connection string for your database server.</span></span>
    2. <span data-ttu-id="49952-131">Pomocí přepínače **– a** určete funkce aplikačních služeb, které chcete přidat do databáze.</span><span class="sxs-lookup"><span data-stu-id="49952-131">Use the **–A** switch to specify the application services features you want to add to the database.</span></span> <span data-ttu-id="49952-132">V takovém případě **m** označuje, že chcete přidat podporu pro poskytovatele členství a **r** označuje, že chcete přidat podporu pro správce rolí.</span><span class="sxs-lookup"><span data-stu-id="49952-132">In this case, **m** indicates that you want to add support for the membership provider and **r** indicates that you want to add support for the role manager.</span></span>
    3. <span data-ttu-id="49952-133">Pomocí přepínače **– d** zadejte název vaší databáze služby Application Services.</span><span class="sxs-lookup"><span data-stu-id="49952-133">Use the **–d** switch to specify a name for your application services database.</span></span> <span data-ttu-id="49952-134">Pokud tento přepínač vynecháte, nástroj vytvoří databázi s výchozím názvem **aspnetdb**.</span><span class="sxs-lookup"><span data-stu-id="49952-134">If you omit this switch, the utility will create a database with the default name of **aspnetdb**.</span></span>
3. <span data-ttu-id="49952-135">Po úspěšném vytvoření databáze se na příkazovém řádku zobrazí potvrzení.</span><span class="sxs-lookup"><span data-stu-id="49952-135">When the database has been created successfully, the command prompt will show a confirmation.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="49952-136">Další informace o nástroji ASPNET\_regsql naleznete v tématu [ASP.NET SQL Server Registration Tool (aspnet\_regsql. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="49952-136">For more information on the aspnet\_regsql utility, see [ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span></span>

<span data-ttu-id="49952-137">V dalším kroku se ujistěte, že připojovací řetězce v řešení Contact Manageru ukazují na vaši místní instanci SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="49952-137">The next step is to make sure that the connection strings in the Contact Manager solution point to your local instance of SQL Server Express.</span></span>

<span data-ttu-id="49952-138">**Aktualizace připojovacích řetězců**</span><span class="sxs-lookup"><span data-stu-id="49952-138">**To update the connection strings**</span></span>

1. <span data-ttu-id="49952-139">Otevřete řešení Contact Manager v aplikaci Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="49952-139">Open the Contact Manager solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="49952-140">V okně **Průzkumník řešení** rozbalte projekt **ContactManager. Mvc** a dvakrát klikněte na uzel **Web. config** .</span><span class="sxs-lookup"><span data-stu-id="49952-140">In the **Solution Explorer** window, expand the **ContactManager.Mvc** project, and then double-click the **Web.config** node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="49952-141">Projekt ContactManager. Mvc obsahuje dva soubory *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="49952-141">The ContactManager.Mvc project includes two *web.config* files.</span></span> <span data-ttu-id="49952-142">Je nutné upravit soubor na úrovni projektu.</span><span class="sxs-lookup"><span data-stu-id="49952-142">You need to edit the project-level file.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. <span data-ttu-id="49952-143">V elementu **connectionStrings** ověřte, zda je připojovací řetězec s názvem **ApplicationServices** Points do místní databáze služby ASP.NET Application Services.</span><span class="sxs-lookup"><span data-stu-id="49952-143">In the **connectionStrings** element, verify that the connection string named **ApplicationServices** points to your local ASP.NET application services database.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. <span data-ttu-id="49952-144">V okně **Průzkumník řešení** rozbalte projekt **ContactManager. Service** a dvakrát klikněte na uzel **Web. config** .</span><span class="sxs-lookup"><span data-stu-id="49952-144">In the **Solution Explorer** window, expand the **ContactManager.Service** project, and then double-click the **Web.config** node.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. <span data-ttu-id="49952-145">V elementu **connectionStrings** v připojovacím řetězci s názvem **ContactManagerContext**ověřte, zda je vlastnost **zdroj dat** nastavena na místní instanci SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="49952-145">In the **connectionStrings** element, in the connection string named **ContactManagerContext**, verify that the **Data Source** property is set to your local instance of SQL Server Express.</span></span> <span data-ttu-id="49952-146">V připojovacím řetězci nemusíte nic dalšího měnit.</span><span class="sxs-lookup"><span data-stu-id="49952-146">You don't need to change anything else in the connection string.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. <span data-ttu-id="49952-147">Uložte všechny otevřené soubory.</span><span class="sxs-lookup"><span data-stu-id="49952-147">Save all open files.</span></span>

<span data-ttu-id="49952-148">Nyní byste měli být připraveni spustit řešení Contact Manager na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="49952-148">You should now be ready to run the Contact Manager solution on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="49952-149">Pokud budete postupovat podle těchto kroků bez předchozího vytvoření databáze služby Application Services, ASP.NET vytvoří databázi při prvním pokusu o vytvoření uživatele.</span><span class="sxs-lookup"><span data-stu-id="49952-149">If you follow these steps without first creating an application services database, ASP.NET will create the database the first time you attempt to create a user.</span></span> <span data-ttu-id="49952-150">Ruční vytvoření databáze ale vám umožní mnohem větší kontrolu nad sadou funkcí služby Application Services, kterou chcete podporovat.</span><span class="sxs-lookup"><span data-stu-id="49952-150">However, manually creating the database gives you a lot more control over the application services feature set you want to support.</span></span>

<span data-ttu-id="49952-151">**Spuštění řešení Contact Manager**</span><span class="sxs-lookup"><span data-stu-id="49952-151">**To run the Contact Manager solution**</span></span>

1. <span data-ttu-id="49952-152">V aplikaci Visual Studio 2010 stiskněte klávesu F5.</span><span class="sxs-lookup"><span data-stu-id="49952-152">In Visual Studio 2010, press F5.</span></span>
2. <span data-ttu-id="49952-153">Spustí se aplikace Internet Explorer a požádá o adresu URL aplikace ASP.NET MVC 3 pro správce kontaktů.</span><span class="sxs-lookup"><span data-stu-id="49952-153">Internet Explorer starts up and requests the URL of the Contact Manager ASP.NET MVC 3 application.</span></span> <span data-ttu-id="49952-154">Ve výchozím nastavení aplikace zobrazí stránku **všechny kontakty** .</span><span class="sxs-lookup"><span data-stu-id="49952-154">By default, the application displays the **All Contacts** page.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. <span data-ttu-id="49952-155">Přidejte několik kontaktů a pak ověřte, že aplikace funguje podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="49952-155">Add a few contacts, and then verify that the application works as expected.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. <span data-ttu-id="49952-156">Přejděte na `http://localhost:50114/Account/Register` (Pokud aplikaci hostuje na jiném portu, upravte adresu URL).</span><span class="sxs-lookup"><span data-stu-id="49952-156">Browse to `http://localhost:50114/Account/Register` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="49952-157">Přidejte uživatelské jméno, e-mailovou adresu a heslo a ověřte, že jste se mohli úspěšně zaregistrovat účet.</span><span class="sxs-lookup"><span data-stu-id="49952-157">Add a user name, email address, and password, and verify that you're able to register an account successfully.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. <span data-ttu-id="49952-158">Přejděte na `http://localhost:50114/Account/LogOn` (Pokud aplikaci hostuje na jiném portu, upravte adresu URL).</span><span class="sxs-lookup"><span data-stu-id="49952-158">Browse to `http://localhost:50114/Account/LogOn` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="49952-159">Ověřte, že jste se mohli přihlásit pomocí účtu, který jste právě vytvořili.</span><span class="sxs-lookup"><span data-stu-id="49952-159">Verify that you're able to log on using the account you just created.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. <span data-ttu-id="49952-160">Ukončete aplikaci Internet Explorer a zastavte ladění.</span><span class="sxs-lookup"><span data-stu-id="49952-160">Close Internet Explorer to stop debugging.</span></span>

## <a name="conclusion"></a><span data-ttu-id="49952-161">Závěr</span><span class="sxs-lookup"><span data-stu-id="49952-161">Conclusion</span></span>

<span data-ttu-id="49952-162">V tomto okamžiku by mělo být řešení Správce kontaktů úplně nakonfigurované tak, aby se spouštělo na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="49952-162">At this point, the Contact Manager solution should be fully configured to run on your local machine.</span></span> <span data-ttu-id="49952-163">Řešení můžete použít jako referenci při práci prostřednictvím dalších témat v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="49952-163">You can use the solution as a reference when you work through the other topics in this tutorial.</span></span>

<span data-ttu-id="49952-164">V dalším tématu [Principy souboru projektu](understanding-the-project-file.md)je vysvětleno, jak můžete použít soubory projektu Custom Microsoft Build Engine (MSBuild) v rámci řešení Správce kontaktů k řízení procesu nasazení.</span><span class="sxs-lookup"><span data-stu-id="49952-164">The next topic, [Understanding the Project File](understanding-the-project-file.md), explains how you can use the custom Microsoft Build Engine (MSBuild) project files within the Contact Manager solution to control the deployment process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="49952-165">[Předchozí](the-contact-manager-solution.md)
> [Další](understanding-the-project-file.md)</span><span class="sxs-lookup"><span data-stu-id="49952-165">[Previous](the-contact-manager-solution.md)
[Next](understanding-the-project-file.md)</span></span>
