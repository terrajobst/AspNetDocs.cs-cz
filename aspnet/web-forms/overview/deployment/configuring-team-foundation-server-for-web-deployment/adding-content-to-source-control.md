---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: Přidávání obsahu do správy zdrojových kódů | Microsoft Docs
author: jrjlee
description: Toto téma vysvětluje, jak přidat obsah do správy zdrojového kódu v Team Foundation Server (TFS) 2010. Popisuje, jak přidat řešení a projekty do týmového projektu...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634461"
---
# <a name="adding-content-to-source-control"></a><span data-ttu-id="8ca2a-104">Přidání obsahu do správy zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="8ca2a-104">Adding Content to Source Control</span></span>

<span data-ttu-id="8ca2a-105">od [Jason Novák](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="8ca2a-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="8ca2a-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="8ca2a-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="8ca2a-107">Toto téma vysvětluje, jak přidat obsah do správy zdrojového kódu v Team Foundation Server (TFS) 2010.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="8ca2a-108">Popisuje, jak přidat řešení a projekty do týmového projektu v TFS a vysvětluje, jak přidat externí závislosti, jako jsou architektury nebo sestavení, do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>

<span data-ttu-id="8ca2a-109">Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="8ca2a-110">Přehled úlohy</span><span class="sxs-lookup"><span data-stu-id="8ca2a-110">Task Overview</span></span>

<span data-ttu-id="8ca2a-111">Ve většině případů by měl být každý člen vývojářského týmu schopný přidávat obsah do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="8ca2a-112">Chcete-li přidat řešení do správy zdrojového kódu v TFS, je nutné provést tyto kroky vysoké úrovně:</span><span class="sxs-lookup"><span data-stu-id="8ca2a-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="8ca2a-113">Připojte se k týmovému projektu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-113">Connect to a team project.</span></span>
- <span data-ttu-id="8ca2a-114">Namapujte strukturu složek týmového projektu na serveru na strukturu složek na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="8ca2a-115">Přidejte řešení a jeho obsah do správy zdrojových kódů.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="8ca2a-116">Přidejte všechny externí závislosti do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="8ca2a-117">V tomto tématu se dozvíte, jak provádět tyto postupy.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="8ca2a-118">V úlohách a návodech v tomto tématu se předpokládá, že jste již vytvořili nový týmový projekt TFS pro správu obsahu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="8ca2a-119">Další informace o vytvoření nového týmového projektu naleznete v tématu [vytvoření týmového projektu v serveru TFS](creating-a-team-project-in-tfs.md).</span><span class="sxs-lookup"><span data-stu-id="8ca2a-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="8ca2a-120">Kdo provádí tyto postupy?</span><span class="sxs-lookup"><span data-stu-id="8ca2a-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="8ca2a-121">Ve většině případů by měl být každý člen vývojářského týmu schopný přidávat a upravovat obsah v rámci konkrétních týmových projektů.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="8ca2a-122">Připojit se k týmovému projektu a vytvořit mapování složky</span><span class="sxs-lookup"><span data-stu-id="8ca2a-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="8ca2a-123">Před přidáním jakéhokoli obsahu do správy zdrojového kódu se musíte připojit k týmovému projektu a vytvořit mapování mezi strukturou složek na serveru a systémem souborů na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="8ca2a-124">**Připojení k týmovému projektu a mapování místní cesty**</span><span class="sxs-lookup"><span data-stu-id="8ca2a-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="8ca2a-125">Na pracovní stanici pro vývojáře otevřete Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="8ca2a-126">V aplikaci Visual Studio v nabídce **tým** klikněte na **připojit k Team Foundation Server**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8ca2a-127">Pokud jste již nakonfigurovali připojení k serveru TFS, můžete vynechat kroky 3-6.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="8ca2a-128">V dialogovém okně **připojení k týmovému projektu** klikněte na možnost **servery**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="8ca2a-129">V dialogovém okně **Přidat/odebrat Team Foundation Server** klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="8ca2a-130">V dialogovém okně **přidat Team Foundation Server** zadejte podrobnosti instance TFS a pak klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="8ca2a-131">V dialogovém okně **Přidat/odebrat Team Foundation Server** klikněte na **Zavřít**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="8ca2a-132">V dialogovém okně **připojit k týmovému projektu** vyberte instanci TFS, ke které se chcete připojit, vyberte kolekci týmového projektu, vyberte týmový projekt, do kterého chcete přidat, a potom klikněte na tlačítko **připojit**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="8ca2a-133">V okně **Team Explorer** rozbalte svůj týmový projekt a potom poklikejte na **Správa zdrojového kódu**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="8ca2a-134">Na kartě **Průzkumník správy zdrojových souborů** klikněte na **Nenamapováno**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="8ca2a-135">V dialogovém okně **Mapa** v poli **místní složka** vyhledejte (nebo vytvořte) místní složku, která bude sloužit jako kořenová složka pro týmový projekt, a pak klikněte na tlačítko **Mapa**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="8ca2a-136">Až budete vyzváni ke stažení zdrojových souborů, klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="8ca2a-137">V tomto okamžiku jste namapovali složku na straně serveru pro týmový projekt do místní složky na pracovní stanici pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="8ca2a-138">Stáhli jste také veškerý existující obsah z týmového projektu do vaší místní struktury složek.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="8ca2a-139">Nyní můžete začít přidávat vlastní obsah do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="8ca2a-140">Přidat projekty a řešení do správy zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="8ca2a-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="8ca2a-141">Chcete-li přidat projekty a řešení do správy zdrojového kódu, je nutné je nejprve přesunout do mapované složky pro týmový projekt na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="8ca2a-142">Potom můžete obsah vrátit se změnami a synchronizovat vaše dodatky se serverem.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="8ca2a-143">**Přidání projektů do správy zdrojových kódů**</span><span class="sxs-lookup"><span data-stu-id="8ca2a-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="8ca2a-144">Na pracovní stanici pro vývojáře přesuňte své projekty a řešení do vhodného umístění v rámci struktury mapované složky pro týmový projekt.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8ca2a-145">Mnoho organizací bude mít upřednostňovaný přístup k tomu, jak by měly být projekty a řešení uspořádány ve správě zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="8ca2a-146">Pokyny k strukturování složek naleznete v tématu [How to: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ca2a-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="8ca2a-147">Otevřete řešení v aplikaci Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="8ca2a-148">V okně **Průzkumník řešení** klikněte pravým tlačítkem na řešení a potom klikněte na **Přidat řešení do správy zdrojového kódu**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="8ca2a-149">V některých případech, v závislosti na tom, jak vaše organizace chce strukturovat obsah v TFS, možná budete muset přidat projekty do správy zdrojového kódu jednotlivě a poskytnout tak přesnější kontrolu nad tím, jak je zdrojový kód uspořádán.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="8ca2a-150">Ověřte, zda se na kartě **Průzkumník správy zdrojových souborů** zobrazuje obsah, který jste přidali v rámci struktury serverové složky pro týmový projekt.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="8ca2a-151">Karta **Průzkumník správy zdrojových souborů** zobrazuje obsah bez dalšího dotazování, protože jste své řešení přidali do mapované složky v místním systému souborů.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="8ca2a-152">Pokud bylo vaše řešení v nemapovaném umístění, zobrazí se výzva k zadání umístění složky v TFS i v místním systému souborů.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="8ca2a-153">Na kartě **Průzkumník správy zdrojových souborů** v podokně **složky** klikněte pravým tlačítkem myši na týmový projekt (například **ContactManager**) a potom klikněte na možnost **vrátit se změnami do seznamu probíhající změny**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="8ca2a-154">V dialogovém okně **vrátit se změnami – zdrojové soubory** zadejte komentář a potom klikněte na možnost **vrátit se**změnami.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="8ca2a-155">V tomto okamžiku jste přidali řešení do správy zdrojového kódu v TFS.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="8ca2a-156">Přidat externí závislosti do správy zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="8ca2a-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="8ca2a-157">Když přidáte projekt nebo řešení do správy zdrojového kódu, budou přidány také všechny soubory a složky v rámci projektu nebo řešení.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="8ca2a-158">V mnoha případech se ale projekty a řešení také spoléhají na externí závislosti, jako jsou místní sestavení, aby fungovaly správně.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="8ca2a-159">Je nutné přidat takové prostředky do správy zdrojových kódů, aby mohl týmový Build i ostatní členové týmu vývojáře sestavit kód úspěšně.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="8ca2a-160">Například struktura složky pro ukázkové řešení Contact Manager obsahuje složku s názvem Packages.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="8ca2a-161">Obsahuje sestavení a různé podpůrné prostředky pro ADO.NET Entity Framework 4,1.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="8ca2a-162">Složka Packages není součástí řešení Správce kontaktů, ale řešení se bez něj nebude sestavovat úspěšně.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="8ca2a-163">Chcete-li povolit týmové sestavení pro sestavení řešení, je nutné přidat složku balíčky do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="8ca2a-164">Zahrnutí složky balíčků je typické, co se stane, když do svého řešení přidáte Entity Framework nebo podobné prostředky pomocí rozšíření NuGet pro Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>

<span data-ttu-id="8ca2a-165">**Přidání jiného než projektového obsahu do správy zdrojů**</span><span class="sxs-lookup"><span data-stu-id="8ca2a-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="8ca2a-166">Ujistěte se, že položky, které chcete přidat (například složka balíčky), jsou v příslušném umístění v rámci mapované složky v místním systému souborů.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="8ca2a-167">V aplikaci Visual Studio 2010 v okně **Team Explorer** rozbalte svůj týmový projekt a dvakrát klikněte na položku **Správa zdrojového kódu**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="8ca2a-168">Na kartě **Průzkumník správy zdrojových souborů** v podokně **složky** vyberte složku obsahující položku nebo položky, které chcete přidat.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="8ca2a-169">Klikněte na tlačítko **Přidat položky do složky** .</span><span class="sxs-lookup"><span data-stu-id="8ca2a-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="8ca2a-170">V dialogovém okně **Přidat do správy zdrojového kódu** vyberte složku nebo položky, které chcete přidat, a poté klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="8ca2a-171">Na kartě **vyloučené položky** vyberte všechny požadované položky, které byly automaticky vyloučeny (například sestavení), a potom klikněte na položku **Zahrnout položky (y)** .</span><span class="sxs-lookup"><span data-stu-id="8ca2a-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="8ca2a-172">Na kartě **položky, které chcete přidat** ověřte, zda jsou uvedeny všechny soubory, které chcete zahrnout, a poté klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="8ca2a-173">V okně **Průzkumník správy zdrojových souborů** klikněte na tlačítko **vrátit se změnami** .</span><span class="sxs-lookup"><span data-stu-id="8ca2a-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="8ca2a-174">V dialogovém okně **vrátit se změnami – zdrojové soubory** zadejte komentář a potom klikněte na možnost **vrátit se**změnami.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="8ca2a-175">V tuto chvíli jste přidali externí závislosti pro vaše řešení do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="8ca2a-176">Závěr</span><span class="sxs-lookup"><span data-stu-id="8ca2a-176">Conclusion</span></span>

<span data-ttu-id="8ca2a-177">Toto téma popisuje, jak se připojit k týmovému projektu, mapovat strukturu složek a přidat obsah do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="8ca2a-178">Další informace o tom, jak pracovat s položkami v rámci správy zdrojového kódu, naleznete v tématu [using a Control Version](https://msdn.microsoft.com/library/ms181368.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ca2a-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

<span data-ttu-id="8ca2a-179">V dalším tématu [Konfigurace serveru TFS Build pro nasazení webu](configuring-a-tfs-build-server-for-web-deployment.md), popisuje, jak připravit server TFS Team Build pro sestavení a nasazení vašeho řešení.</span><span class="sxs-lookup"><span data-stu-id="8ca2a-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="8ca2a-180">Další čtení</span><span class="sxs-lookup"><span data-stu-id="8ca2a-180">Further Reading</span></span>

<span data-ttu-id="8ca2a-181">Další informace o práci se správou zdrojového kódu v TFS najdete v tématu [použití správy verzí](https://msdn.microsoft.com/library/ms181368.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ca2a-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8ca2a-182">[Předchozí](creating-a-team-project-in-tfs.md)
> [Další](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="8ca2a-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>
