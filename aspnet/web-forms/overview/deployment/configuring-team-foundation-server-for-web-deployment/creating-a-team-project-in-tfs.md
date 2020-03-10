---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: Vytvoření týmového projektu v TFS | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak vytvořit nový týmový projekt v Team Foundation Server (TFS) 2010.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639655"
---
# <a name="creating-a-team-project-in-tfs"></a><span data-ttu-id="6da87-103">Vytváření týmových projektů v TFS</span><span class="sxs-lookup"><span data-stu-id="6da87-103">Creating a Team Project in TFS</span></span>

<span data-ttu-id="6da87-104">od [Jason Novák](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="6da87-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="6da87-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="6da87-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="6da87-106">Toto téma popisuje, jak vytvořit nový týmový projekt v Team Foundation Server (TFS) 2010.</span><span class="sxs-lookup"><span data-stu-id="6da87-106">This topic describes how to create a new team project in Team Foundation Server (TFS) 2010.</span></span>

<span data-ttu-id="6da87-107">Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.</span><span class="sxs-lookup"><span data-stu-id="6da87-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="6da87-108">Přehled úlohy</span><span class="sxs-lookup"><span data-stu-id="6da87-108">Task Overview</span></span>

<span data-ttu-id="6da87-109">Chcete-li zřídit a použít nový týmový projekt na serveru TFS, je nutné provést tyto kroky vysoké úrovně:</span><span class="sxs-lookup"><span data-stu-id="6da87-109">To provision and use a new team project in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="6da87-110">Udělte oprávnění uživateli, který vytvoří nový týmový projekt.</span><span class="sxs-lookup"><span data-stu-id="6da87-110">Grant permissions to the user who will create the new team project.</span></span>
- <span data-ttu-id="6da87-111">Vytvořte týmový projekt.</span><span class="sxs-lookup"><span data-stu-id="6da87-111">Create the team project.</span></span>
- <span data-ttu-id="6da87-112">Udělte oprávnění členům týmu, kteří budou pracovat na projektu.</span><span class="sxs-lookup"><span data-stu-id="6da87-112">Grant permissions to the team members who will work on the project.</span></span>
- <span data-ttu-id="6da87-113">Vrátit se změnami obsah.</span><span class="sxs-lookup"><span data-stu-id="6da87-113">Check in some content.</span></span>

<span data-ttu-id="6da87-114">V tomto tématu se dozvíte, jak provádět tyto postupy, a identifikuje uživatele a role úloh, které jsou pravděpodobně zodpovědné za jednotlivé postupy.</span><span class="sxs-lookup"><span data-stu-id="6da87-114">This topic will show you how to perform these procedures, and it will identify the users and job roles that are likely to be responsible for each procedure.</span></span> <span data-ttu-id="6da87-115">Uvědomte si, že v závislosti na struktuře vaší organizace může být každý z těchto úkolů zodpovědností jiné osoby.</span><span class="sxs-lookup"><span data-stu-id="6da87-115">Be aware that, depending on the structure of your organization, each of these tasks may be the responsibility of a different person.</span></span>

<span data-ttu-id="6da87-116">V úlohách a návodech v tomto tématu se předpokládá, že jste nainstalovali a nakonfigurovali TFS a že jste jako součást procesu konfigurace vytvořili kolekci týmového projektu.</span><span class="sxs-lookup"><span data-stu-id="6da87-116">The tasks and walkthroughs in this topic assume that you've installed and configured TFS, and that you've created a team project collection as part of the configuration process.</span></span> <span data-ttu-id="6da87-117">Další informace o těchto předpokladech a obecnější informace o tomto scénáři najdete v tématu [Konfigurace serveru TFS Build pro nasazení webu](configuring-a-tfs-build-server-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="6da87-117">For more information on these assumptions, and for more general background information on the scenario, see [Configure a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span>

## <a name="grant-permissions-to-the-team-project-creator"></a><span data-ttu-id="6da87-118">Udělení oprávnění tvůrci týmového projektu</span><span class="sxs-lookup"><span data-stu-id="6da87-118">Grant Permissions to the Team Project Creator</span></span>

<span data-ttu-id="6da87-119">Pro vytvoření nového týmového projektu budete potřebovat tato oprávnění:</span><span class="sxs-lookup"><span data-stu-id="6da87-119">In order to create a new team project, you need these permissions:</span></span>

- <span data-ttu-id="6da87-120">Musíte mít oprávnění **vytvořit nové projekty** v aplikační vrstvě TFS.</span><span class="sxs-lookup"><span data-stu-id="6da87-120">You must have the **Create new projects** permission on the TFS application tier.</span></span> <span data-ttu-id="6da87-121">Toto oprávnění obvykle udělujete přidáním uživatelů do skupiny TFS **Správci kolekce projektů** .</span><span class="sxs-lookup"><span data-stu-id="6da87-121">You typically grant this permission by adding users to the **Project Collection Administrators** TFS group.</span></span> <span data-ttu-id="6da87-122">Toto oprávnění zahrnuje i globální skupina **Správci Team Foundation** .</span><span class="sxs-lookup"><span data-stu-id="6da87-122">The **Team Foundation Administrators** global group also includes this permission.</span></span>
- <span data-ttu-id="6da87-123">Musíte mít oprávnění k vytváření nových týmových webů v rámci kolekce webů služby SharePoint, která odpovídá kolekci TFS Team Project Collection.</span><span class="sxs-lookup"><span data-stu-id="6da87-123">You must have permission to create new team sites within the SharePoint site collection that corresponds to the TFS team project collection.</span></span> <span data-ttu-id="6da87-124">Toto oprávnění obvykle udělujete tak, že přidáte uživatele do skupiny služby SharePoint s právy **Úplné řízení** v kolekci webů služby SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6da87-124">You typically grant this permission by adding the user to a SharePoint group with **Full Control** rights on the SharePoint site collection.</span></span>
- <span data-ttu-id="6da87-125">Pokud používáte funkce SQL Server Reporting Services, musíte být členem role **Správce obsahu Team Foundation** ve službě Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="6da87-125">If you're using SQL Server Reporting Services features, you must be a member of the **Team Foundation Content Manager** role in Reporting Services.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="6da87-126">Kdo provádí tyto postupy?</span><span class="sxs-lookup"><span data-stu-id="6da87-126">Who Performs These Procedures?</span></span>

<span data-ttu-id="6da87-127">Obvykle tyto postupy provádí osoba nebo skupina, která spravuje nasazení TFS.</span><span class="sxs-lookup"><span data-stu-id="6da87-127">Typically, the person or group who administers the TFS deployment also performs these procedures.</span></span>

<span data-ttu-id="6da87-128">Vzhledem k tomu, že se jedná o vysoce privilegovanou sadu oprávnění, jsou nové týmové projekty obvykle vytvářeny malou podmnožinou uživatelů s zodpovědností za správu nasazení serveru TFS.</span><span class="sxs-lookup"><span data-stu-id="6da87-128">Because this is a highly privileged set of permissions, new team projects are typically created by a small subset of users with responsibility for administering a TFS deployment.</span></span> <span data-ttu-id="6da87-129">Vývojářům většinou nebudou udělena oprávnění potřebná k vytváření nových týmových projektů.</span><span class="sxs-lookup"><span data-stu-id="6da87-129">Developers will not usually be granted the permissions required to create new team projects.</span></span>

### <a name="grant-permissions-in-tfs"></a><span data-ttu-id="6da87-130">Udělení oprávnění v TFS</span><span class="sxs-lookup"><span data-stu-id="6da87-130">Grant Permissions in TFS</span></span>

<span data-ttu-id="6da87-131">Chcete-li uživateli povolit vytváření nových týmových projektů, je prvním úkolem vysoké úrovně přidání uživatele do skupiny **Správci kolekcí projektů** pro kolekci týmového projektu.</span><span class="sxs-lookup"><span data-stu-id="6da87-131">If you want to enable a user to create new team projects, the first high-level task is to add the user to the **Project Collection Administrators** group for the team project collection.</span></span>

<span data-ttu-id="6da87-132">**Přidání uživatele do skupiny Správci kolekcí projektů**</span><span class="sxs-lookup"><span data-stu-id="6da87-132">**To add a user to the Project Collection Administrators group**</span></span>

1. <span data-ttu-id="6da87-133">Na serveru TFS v nabídce **Start** přejděte na **všechny programy**, klikněte na **Microsoft Team Foundation Server 2010**a potom klikněte na **Konzola pro správu serveru Team Foundation**.</span><span class="sxs-lookup"><span data-stu-id="6da87-133">On the TFS server, on the **Start** menu, point to **All Programs**, click **Microsoft Team Foundation Server 2010**, and then click **Team Foundation Administration Console**.</span></span>
2. <span data-ttu-id="6da87-134">Ve stromovém zobrazení rozbalte položku **aplikační vrstva**a potom klikněte na položku **kolekce týmových projektů**.</span><span class="sxs-lookup"><span data-stu-id="6da87-134">In the navigation tree view, expand **Application Tier**, and then click **Team Project Collections**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. <span data-ttu-id="6da87-135">V podokně **kolekce týmových projektů** vyberte kolekci týmového projektu, kterou chcete spravovat.</span><span class="sxs-lookup"><span data-stu-id="6da87-135">In the **Team Project Collections** pane, select the team project collection you want to manage.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. <span data-ttu-id="6da87-136">Na kartě **Obecné** klikněte na **členství ve skupině**.</span><span class="sxs-lookup"><span data-stu-id="6da87-136">On the **General** tab, click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. <span data-ttu-id="6da87-137">V dialogovém okně **globální skupiny** vyberte skupinu **Správci kolekce projektů** a potom klikněte na tlačítko **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="6da87-137">In the **Global Groups** dialog box, select the **Project Collection Administrators** group, and then click **Properties**.</span></span>
6. <span data-ttu-id="6da87-138">V dialogovém okně **Vlastnosti skupiny Team Foundation Server** vyberte **uživatele nebo skupinu systému Windows**a potom klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6da87-138">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. <span data-ttu-id="6da87-139">V dialogovém okně **Vybrat uživatele, počítače nebo skupiny** zadejte uživatelské jméno uživatele, kterého chcete umožnit vytváření nových týmových projektů, klikněte na tlačítko **kontrolovat názvy**a pak klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="6da87-139">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to be able to create new team projects, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. <span data-ttu-id="6da87-140">V dialogovém okně **Vlastnosti skupiny Team Foundation Server** klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="6da87-140">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
9. <span data-ttu-id="6da87-141">V dialogovém okně **globální skupiny** klikněte na **Zavřít**.</span><span class="sxs-lookup"><span data-stu-id="6da87-141">In the **Global Groups** dialog box, click **Close**.</span></span>

### <a name="grant-permissions-in-sharepoint-services"></a><span data-ttu-id="6da87-142">Udělení oprávnění ve službě SharePoint Services</span><span class="sxs-lookup"><span data-stu-id="6da87-142">Grant Permissions in SharePoint Services</span></span>

<span data-ttu-id="6da87-143">Dále musíte uživateli udělit oprávnění k vytváření nových týmových webů v kolekci webů služby SharePoint, která odpovídá vaší kolekci týmových projektů TFS.</span><span class="sxs-lookup"><span data-stu-id="6da87-143">Next, you need to give the user permission to create new team sites in the SharePoint site collection that corresponds to your TFS team project collection.</span></span>

<span data-ttu-id="6da87-144">**Udělení oprávnění k úplnému řízení pro kolekci webů služby SharePoint**</span><span class="sxs-lookup"><span data-stu-id="6da87-144">**To grant Full Control permissions on the SharePoint site collection**</span></span>

1. <span data-ttu-id="6da87-145">V Team Foundation Server Administration Console na stránce **kolekce týmových projektů** vyberte kolekci týmového projektu, kterou chcete spravovat.</span><span class="sxs-lookup"><span data-stu-id="6da87-145">In the Team Foundation Server Administration Console, on the **Team Project Collections** page, select the team project collection you want to manage.</span></span>
2. <span data-ttu-id="6da87-146">Na kartě **sharepointový web** si poznamenejte hodnotu **aktuální výchozí umístění lokality** adresa URL.</span><span class="sxs-lookup"><span data-stu-id="6da87-146">On the **SharePoint Site** tab, note the value of the **Current Default Site Location** URL.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. <span data-ttu-id="6da87-147">Spusťte aplikaci Internet Explorer a pak použijte adresu URL, kterou jste si poznamenali v kroku 2.</span><span class="sxs-lookup"><span data-stu-id="6da87-147">Open Internet Explorer, and then go to the URL you noted in step 2.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6da87-148">Pokud nejste přihlášení k Windows jako uživatel, který kolekci týmových projektů vytvořil, budete se muset přihlásit k SharePointu jako tento uživatel, aby bylo možné pokračovat.</span><span class="sxs-lookup"><span data-stu-id="6da87-148">If you're not logged on to Windows as the user who created the team project collection, you'll need to sign in to SharePoint as this user in order to continue.</span></span>
4. <span data-ttu-id="6da87-149">V nabídce **Akce webu** klikněte na položku **Nastavení webu**.</span><span class="sxs-lookup"><span data-stu-id="6da87-149">On the **Site Actions** menu, click **Site Settings**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. <span data-ttu-id="6da87-150">Na stránce **Nastavení webu** v části **Uživatelé a oprávnění**klikněte na **Uživatelé a skupiny**.</span><span class="sxs-lookup"><span data-stu-id="6da87-150">On the **Site Settings** page, under **Users and Permissions**, click **People and groups**.</span></span>
6. <span data-ttu-id="6da87-151">V levém navigačním panelu klikněte na **skupiny**.</span><span class="sxs-lookup"><span data-stu-id="6da87-151">In the left navigation panel, click **Groups**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. <span data-ttu-id="6da87-152">Na stránce **lidé a skupiny: všechny skupiny** klikněte na **nastavit skupiny pro tento web**.</span><span class="sxs-lookup"><span data-stu-id="6da87-152">On the **People and Groups: All Groups** page, click **Set Up Groups for this Site**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > <span data-ttu-id="6da87-153">Může se zobrazit chyba <strong>HTTP 404 nenalezena</strong> z důvodu chyby kódování http s dvojitou přesností.</span><span class="sxs-lookup"><span data-stu-id="6da87-153">You may receive an <strong>HTTP 404 Not Found</strong> error due to a double HTTP encoding bug.</span></span> <span data-ttu-id="6da87-154">Pokud k tomu dojde, nahraďte adresu URL tímto:</span><span class="sxs-lookup"><span data-stu-id="6da87-154">If this occurs, replace the URL with this:</span></span>   
   > <span data-ttu-id="6da87-155">`[site_collection_URL]/_layouts/permsetup.aspx` například:</span><span class="sxs-lookup"><span data-stu-id="6da87-155">`[site_collection_URL]/_layouts/permsetup.aspx` For example:</span></span>  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. <span data-ttu-id="6da87-156">Na stránce **nastavit skupiny pro tuto lokalitu** přidejte uživatele, který bude vytvářet týmové projekty, do skupiny **vlastníci** a pak klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="6da87-156">On the **Set Up Groups for this Site** page, add the user who will create team projects to the **Owners** group, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image10.png)

<span data-ttu-id="6da87-157">Další informace o tom, jak povolit uživatelům vytvářet nové týmové projekty v rámci kolekce týmového projektu, naleznete v tématu [Nastavení oprávnění správce pro kolekce týmových projektů](https://msdn.microsoft.com/library/dd547204.aspx).</span><span class="sxs-lookup"><span data-stu-id="6da87-157">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span>

## <a name="create-a-new-team-project-and-add-users"></a><span data-ttu-id="6da87-158">Vytvoření nového týmového projektu a přidání uživatelů</span><span class="sxs-lookup"><span data-stu-id="6da87-158">Create a New Team Project and Add Users</span></span>

<span data-ttu-id="6da87-159">Jakmile máte potřebná oprávnění, můžete použít okno **Team Explorer** v aplikaci Visual Studio 2010 k vytvoření nového týmového projektu.</span><span class="sxs-lookup"><span data-stu-id="6da87-159">Once you have the necessary permissions, you can use the **Team Explorer** window in Visual Studio 2010 to create a new team project.</span></span> <span data-ttu-id="6da87-160">Tento přístup poskytuje průvodce, který shromažďuje všechny požadované informace a provádí nezbytné úlohy v TFS, SharePointu a SQL Server Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="6da87-160">This approach provides a wizard that collects all the required information and performs the necessary tasks in TFS, SharePoint, and SQL Server Reporting Services.</span></span> <span data-ttu-id="6da87-161">Také budete muset udělit oprávnění k novému týmovému projektu členům vývojářského týmu, aby jim umožnili přidávat a upravovat obsah.</span><span class="sxs-lookup"><span data-stu-id="6da87-161">You'll also need to grant permissions on the new team project to members of the developer team, to enable them to add and modify content.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="6da87-162">Kdo provádí tyto postupy?</span><span class="sxs-lookup"><span data-stu-id="6da87-162">Who Performs These Procedures?</span></span>

<span data-ttu-id="6da87-163">Tyto postupy obvykle provádí správce TFS nebo vedoucí vývojářského týmu.</span><span class="sxs-lookup"><span data-stu-id="6da87-163">Usually either a TFS administrator or a developer team leader performs these procedures.</span></span>

### <a name="create-a-new-team-project"></a><span data-ttu-id="6da87-164">Vytvořit nový týmový projekt</span><span class="sxs-lookup"><span data-stu-id="6da87-164">Create a New Team Project</span></span>

<span data-ttu-id="6da87-165">Další postup popisuje, jak vytvořit nový týmový projekt v TFS 2010.</span><span class="sxs-lookup"><span data-stu-id="6da87-165">The next procedure describes how to create a new team project in TFS 2010.</span></span>

<span data-ttu-id="6da87-166">**Vytvoření nového týmového projektu**</span><span class="sxs-lookup"><span data-stu-id="6da87-166">**To create a new team project**</span></span>

1. <span data-ttu-id="6da87-167">V nabídce **Start** přejděte na **všechny programy**, klikněte na **Microsoft Visual Studio 2010**, klikněte pravým tlačítkem na **Microsoft Visual Studio 2010**a pak klikněte na **Spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="6da87-167">On the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, right-click **Microsoft Visual Studio 2010**, and then click **Run as administrator**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6da87-168">Pokud Visual Studio 2010 nespouštíte jako správce, Průvodce novým týmovým projektem se v posledním kroku nezdařil.</span><span class="sxs-lookup"><span data-stu-id="6da87-168">If you don't run Visual Studio 2010 as an administrator, the New Team Project Wizard will fail on the last step.</span></span>
2. <span data-ttu-id="6da87-169">Pokud se zobrazí dialogové okno **řízení uživatelských účtů** , klikněte na tlačítko **Ano**.</span><span class="sxs-lookup"><span data-stu-id="6da87-169">If the **User Account Control** dialog box appears, click **Yes**.</span></span>
3. <span data-ttu-id="6da87-170">V aplikaci Visual Studio v nabídce **tým** klikněte na **připojit k Team Foundation Server**.</span><span class="sxs-lookup"><span data-stu-id="6da87-170">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6da87-171">Pokud jste již nakonfigurovali připojení k serveru TFS, můžete vynechat kroky 4-7.</span><span class="sxs-lookup"><span data-stu-id="6da87-171">If you have already configured a connection to a TFS server, you can omit steps 4-7.</span></span>
4. <span data-ttu-id="6da87-172">V dialogovém okně **připojení k týmovému projektu** klikněte na možnost **servery**.</span><span class="sxs-lookup"><span data-stu-id="6da87-172">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
5. <span data-ttu-id="6da87-173">V dialogovém okně **Přidat/odebrat Team Foundation Server** klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6da87-173">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
6. <span data-ttu-id="6da87-174">V dialogovém okně **přidat Team Foundation Server** zadejte podrobnosti instance TFS a pak klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="6da87-174">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. <span data-ttu-id="6da87-175">V dialogovém okně **Přidat/odebrat Team Foundation Server** klikněte na **Zavřít**.</span><span class="sxs-lookup"><span data-stu-id="6da87-175">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
8. <span data-ttu-id="6da87-176">V dialogovém okně **připojit k týmovému projektu** vyberte instanci TFS, ke které se chcete připojit, vyberte kolekci týmového projektu, do které chcete přidat, a poté klikněte na tlačítko **připojit**.</span><span class="sxs-lookup"><span data-stu-id="6da87-176">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection you want to add to, and then click **Connect**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. <span data-ttu-id="6da87-177">V okně **Team Explorer** klikněte pravým tlačítkem na kolekci týmového projektu a pak klikněte na **nový týmový projekt**.</span><span class="sxs-lookup"><span data-stu-id="6da87-177">In the **Team Explorer** window, right-click the team project collection, and then click **New Team Project**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. <span data-ttu-id="6da87-178">V dialogovém okně **nový týmový projekt** zadejte název a popis týmového projektu a poté klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="6da87-178">In the **New Team Project** dialog box, provide a name and a description for the team project, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6da87-179">Pokud váš týmový projekt obsahuje mezery, můžete se setkat s některými problémy při použití nástroje Internetová informační služba (IIS) web pro nasazení webu (Nasazení webu) k nasazení balíčků z výstupní cesty.</span><span class="sxs-lookup"><span data-stu-id="6da87-179">If your team project includes spaces, you may face some issues when you come to use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy packages from the output path.</span></span> <span data-ttu-id="6da87-180">Mezery v cestě můžou mít za následek mnohem obtížnější spuštění Nasazení webuch příkazů.</span><span class="sxs-lookup"><span data-stu-id="6da87-180">Spaces in the path can make it a lot more difficult to run Web Deploy commands.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. <span data-ttu-id="6da87-181">Na stránce **Vyberte šablonu procesu** vyberte šablonu procesu, kterou chcete použít ke správě procesu vývoje, a poté klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="6da87-181">On the **Select a Process Template** page, select the process template that you want to use to manage the development process, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6da87-182">Další informace o šablonách procesů pro TFS naleznete v tématu [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).</span><span class="sxs-lookup"><span data-stu-id="6da87-182">For more information on process templates for TFS, see [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).</span></span>
12. <span data-ttu-id="6da87-183">Na stránce **nastavení týmového webu** ponechte výchozí nastavení beze změny a potom klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="6da87-183">On the **Team Site Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
13. <span data-ttu-id="6da87-184">Toto nastavení vytvoří nebo identifikuje týmový web služby SharePoint, který je spojen s týmovým projektem TFS.</span><span class="sxs-lookup"><span data-stu-id="6da87-184">This setting creates, or identifies, a SharePoint team site that is associated with the TFS team project.</span></span> <span data-ttu-id="6da87-185">Váš vývojový tým může pomocí tohoto webu spravovat dokumentaci, zúčastnit se diskuzních vláken, vytvářet stránky wikiwebu a provádět různé další úkoly, které nesouvisí s kódem.</span><span class="sxs-lookup"><span data-stu-id="6da87-185">Your development team can use this site to manage documentation, participate in discussion threads, create wiki pages, and perform various other tasks that are not related to code.</span></span> <span data-ttu-id="6da87-186">Další informace najdete v tématu [interakce mezi produkty SharePoint a Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span><span class="sxs-lookup"><span data-stu-id="6da87-186">For more information, see [Interactions Between SharePoint Products and Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span></span>
14. <span data-ttu-id="6da87-187">Na stránce **zadat nastavení správy zdrojů** ponechte výchozí nastavení beze změny a potom klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="6da87-187">On the **Specify Source Control Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
15. <span data-ttu-id="6da87-188">Toto nastavení identifikuje nebo vytvoří umístění v hierarchii složek TFS, které bude sloužit jako kořenová složka pro váš obsah.</span><span class="sxs-lookup"><span data-stu-id="6da87-188">This setting identifies or creates the location in the TFS folder hierarchy that will act as a root folder for your content.</span></span>
16. <span data-ttu-id="6da87-189">Na stránce **Potvrdit nastavení týmového projektu** klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="6da87-189">On the **Confirm Team Project Settings** page, click **Finish**.</span></span>
17. <span data-ttu-id="6da87-190">Po úspěšném vytvoření nového týmového projektu klikněte na stránce **vytvořený týmový projekt** na **Zavřít**.</span><span class="sxs-lookup"><span data-stu-id="6da87-190">When the new team project is successfully created, on the **Team Project Created** page, click **Close**.</span></span>

### <a name="add-users-to-a-team-project"></a><span data-ttu-id="6da87-191">Přidání uživatelů do týmového projektu</span><span class="sxs-lookup"><span data-stu-id="6da87-191">Add Users to a Team Project</span></span>

<span data-ttu-id="6da87-192">Teď, když jste vytvořili nový týmový projekt, můžete uživatelům udělit oprávnění k tomu, aby mohli začít přidávat a spolupracovat na obsahu.</span><span class="sxs-lookup"><span data-stu-id="6da87-192">Now that you've created the new team project, you can grant permissions to users to enable them to start adding and collaborating on content.</span></span>

<span data-ttu-id="6da87-193">**Přidání uživatelů do týmového projektu**</span><span class="sxs-lookup"><span data-stu-id="6da87-193">**To add users to a team project**</span></span>

1. <span data-ttu-id="6da87-194">V aplikaci Visual Studio 2010 v okně **Team Explorer** klikněte pravým tlačítkem myši na týmový projekt, přejděte na položku **nastavení týmového projektu**a pak klikněte na položku **členství ve skupině**.</span><span class="sxs-lookup"><span data-stu-id="6da87-194">In Visual Studio 2010, in the **Team Explorer** window, right-click the team project, point to **Team Project Settings**, and then click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. <span data-ttu-id="6da87-195">Chcete-li uživateli povolit přidávání, úpravy a odebírání kódu pod správou zdrojových kódů, je nutné jej přidat do skupiny **přispěvatelé** .</span><span class="sxs-lookup"><span data-stu-id="6da87-195">To enable a user to add, modify, and remove code under source control, you need to add him or her to the **Contributors** group.</span></span>
3. <span data-ttu-id="6da87-196">V dialogovém okně **skupiny projektu** vyberte skupinu **přispěvatelé** a potom klikněte na tlačítko **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="6da87-196">In the **Project Groups** dialog box, select the **Contributors** group, and then click **Properties**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. <span data-ttu-id="6da87-197">V dialogovém okně **Vlastnosti skupiny Team Foundation Server** vyberte **uživatele nebo skupinu systému Windows**a potom klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="6da87-197">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. <span data-ttu-id="6da87-198">V dialogovém okně **Vybrat uživatele, počítače nebo skupiny** zadejte uživatelské jméno uživatele, kterého chcete přidat do týmového projektu, klikněte na tlačítko **kontrolovat jména**a potom klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="6da87-198">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to add to the team project, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. <span data-ttu-id="6da87-199">V dialogovém okně **Vlastnosti skupiny Team Foundation Server** klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="6da87-199">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
7. <span data-ttu-id="6da87-200">V dialogovém okně **skupiny projektu** klikněte na tlačítko **Zavřít**.</span><span class="sxs-lookup"><span data-stu-id="6da87-200">In the **Project Groups** dialog box, click **Close**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="6da87-201">Závěr</span><span class="sxs-lookup"><span data-stu-id="6da87-201">Conclusion</span></span>

<span data-ttu-id="6da87-202">V tuto chvíli je váš nový týmový projekt připravený k použití a váš vývojový tým může začít přidávat obsah a spolupracovat na procesu vývoje.</span><span class="sxs-lookup"><span data-stu-id="6da87-202">At this point, your new team project is ready to use, and your developer team can start adding content and collaborating on the development process.</span></span>

<span data-ttu-id="6da87-203">V dalším tématu [Přidání obsahu do správy zdrojových kódů](adding-content-to-source-control.md)popisuje, jak přidat obsah do správy zdrojových kódů.</span><span class="sxs-lookup"><span data-stu-id="6da87-203">The next topic, [Adding Content to Source Control](adding-content-to-source-control.md), describes how to add content to source control.</span></span>

## <a name="further-reading"></a><span data-ttu-id="6da87-204">Další čtení</span><span class="sxs-lookup"><span data-stu-id="6da87-204">Further Reading</span></span>

<span data-ttu-id="6da87-205">Širší pokyny týkající se vytváření týmových projektů v TFS naleznete v tématu [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="6da87-205">For broader guidance on creating team projects in TFS, see [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span></span> <span data-ttu-id="6da87-206">Další informace o tom, jak povolit uživatelům vytvářet nové týmové projekty v rámci kolekce týmového projektu, naleznete v tématu [Nastavení oprávnění správce pro kolekce týmových projektů](https://msdn.microsoft.com/library/dd547204.aspx).</span><span class="sxs-lookup"><span data-stu-id="6da87-206">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span> <span data-ttu-id="6da87-207">Další informace o přidávání uživatelů do týmových projektů naleznete v tématu [Přidání uživatelů do týmových projektů](https://msdn.microsoft.com/library/bb558971.aspx).</span><span class="sxs-lookup"><span data-stu-id="6da87-207">For more information on adding users to team projects, see [Add Users to Team Projects](https://msdn.microsoft.com/library/bb558971.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6da87-208">[Předchozí](configuring-team-foundation-server-for-web-deployment.md)
> [Další](adding-content-to-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="6da87-208">[Previous](configuring-team-foundation-server-for-web-deployment.md)
[Next](adding-content-to-source-control.md)</span></span>
