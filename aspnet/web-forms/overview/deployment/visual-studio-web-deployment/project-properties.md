---
uid: web-forms/overview/deployment/visual-studio-web-deployment/project-properties
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: Vlastnosti projektu | Dokumentace Microsoftu'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) technologie ASP.NET webové aplikace do Azure App Service Web Apps nebo k poskytovateli hostingu třetích stran, podle usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ec1cec4c-a75f-47af-a2ba-b1e2f971d24b
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/project-properties
msc.type: authoredcontent
ms.openlocfilehash: 85b2aa982c56f030c2de0f3ac2ad0dca780f3f38
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57074143"
---
<a name="aspnet-web-deployment-using-visual-studio-project-properties"></a><span data-ttu-id="52f82-103">Nasazení webu ASP.NET pomocí sady Visual Studio: Vlastnosti projektu</span><span class="sxs-lookup"><span data-stu-id="52f82-103">ASP.NET Web Deployment using Visual Studio: Project Properties</span></span>
====================
<span data-ttu-id="52f82-104">podle [Petr Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="52f82-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="52f82-105">Stáhnout počáteční projekt</span><span class="sxs-lookup"><span data-stu-id="52f82-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="52f82-106">V této sérii kurzů se dozvíte, jak nasadit (publikovat) technologie ASP.NET webové aplikace do Azure App Service Web Apps nebo k poskytovateli hostingu třetích stran, s použitím sady Visual Studio 2012 nebo Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="52f82-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="52f82-107">Informace o této sérii, naleznete v tématu [z prvního kurzu této série](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52f82-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="52f82-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="52f82-108">Overview</span></span>

<span data-ttu-id="52f82-109">Některé možnosti nasazení jsou nakonfigurovány ve vlastnostech projektu, které jsou uloženy v souboru projektu ( *.csproj* nebo *.vbproj* souboru).</span><span class="sxs-lookup"><span data-stu-id="52f82-109">Some deployment options are configured in project properties that are stored in the project file (the *.csproj* or *.vbproj* file).</span></span> <span data-ttu-id="52f82-110">Ve většině případů jsou výchozí hodnoty z těchto nastavení, co chcete, ale můžete použít **vlastnosti projektu** uživatelského rozhraní, které jsou součástí Visual Studia pro práci s těmito nastaveními Pokud máte, tím je Změníme.</span><span class="sxs-lookup"><span data-stu-id="52f82-110">In most cases, the default values of these settings are what you want, but you can use the **Project Properties** UI built into Visual Studio to work with these settings if you have to change them.</span></span> <span data-ttu-id="52f82-111">V tomto kurzu zkontrolujete nastavení nasazení v **vlastnosti projektu**.</span><span class="sxs-lookup"><span data-stu-id="52f82-111">In this tutorial you review the deployment settings in **Project Properties**.</span></span> <span data-ttu-id="52f82-112">Můžete také vytvořit zástupný soubor, který způsobí, že prázdnou složku pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="52f82-112">You also create a placeholder file that causes an empty folder to be deployed.</span></span>

## <a name="configure-deployment-settings-in-the-project-properties-window"></a><span data-ttu-id="52f82-113">Konfigurovat nastavení nasazení v okně Vlastnosti projektu</span><span class="sxs-lookup"><span data-stu-id="52f82-113">Configure deployment settings in the project properties window</span></span>

<span data-ttu-id="52f82-114">Většinu nastavení, které ovlivňují, co se stane během nasazení jsou zahrnuty v profilu publikování, jak uvidíte v následujících kurzech.</span><span class="sxs-lookup"><span data-stu-id="52f82-114">Most settings that affect what happens during deployment are included in the publish profile, as you'll see in the following tutorials.</span></span> <span data-ttu-id="52f82-115">Několik nastavení, které byste měli vědět, jsou umístěny v **balení/publikování** karet **vlastnosti projektu** okna.</span><span class="sxs-lookup"><span data-stu-id="52f82-115">A few settings that you should be aware of are located in the **Package/Publish** tabs of the **Project Properties** window.</span></span> <span data-ttu-id="52f82-116">Tato nastavení jsou zadány pro každou konfiguraci sestavení – to znamená, mohou mít různá nastavení pro sestavení pro vydání, než kolik máte pro sestavení pro ladění.</span><span class="sxs-lookup"><span data-stu-id="52f82-116">These settings are specified for each build configuration — that is, you can have different settings for a Release build than you have for a Debug build.</span></span>

<span data-ttu-id="52f82-117">V **Průzkumníku řešení**, klikněte pravým tlačítkem myši **ContosoUniversity** projekt, vyberte **vlastnosti**a pak vyberte **balení/publikování webu**kartu.</span><span class="sxs-lookup"><span data-stu-id="52f82-117">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Properties**, and then select the **Package/Publish Web** tab.</span></span>

![Kartě Balení/publikování webu](project-properties/_static/image1.png)

<span data-ttu-id="52f82-119">Pokud se zobrazí v okně, použije se výchozí zobrazuje nastavení konfigurace podle toho, která sestavení je aktuálně aktivních pro řešení.</span><span class="sxs-lookup"><span data-stu-id="52f82-119">When the window is displayed, it defaults to showing settings for whichever build configuration is currently active for the solution.</span></span> <span data-ttu-id="52f82-120">Pokud **konfigurace** pole nenaznačuje, že **aktivní (verze)** vyberte **vydání** mohla zobrazit nastavení konfigurace sestavení pro vydání.</span><span class="sxs-lookup"><span data-stu-id="52f82-120">If the **Configuration** box does not indicate **Active (Release)**, select **Release** in order to display settings for the Release build configuration.</span></span> <span data-ttu-id="52f82-121">Sestavení pro vydání budete nasazovat do testovacích i produkčních prostředí.</span><span class="sxs-lookup"><span data-stu-id="52f82-121">You'll deploy Release builds to both your test and production environments.</span></span>

![Výběr konfigurace sestavení pro vydání](project-properties/_static/image2.png)

<span data-ttu-id="52f82-123">S **aktivní (verze)** nebo **vydání** vybrali, se zobrazí hodnoty, které platí při nasazení pomocí konfigurace verze sestavení:</span><span class="sxs-lookup"><span data-stu-id="52f82-123">With **Active (Release)** or **Release** selected, you see the values that are effective when you deploy using the Release build configuration:</span></span>

- <span data-ttu-id="52f82-124">V **položky, které chcete nasadit** pole **pouze soubory potřebné ke spuštění aplikace** zaškrtnuto.</span><span class="sxs-lookup"><span data-stu-id="52f82-124">In the **Items to deploy** box, **Only files needed to run the application** is selected.</span></span> <span data-ttu-id="52f82-125">Další možnosti jsou **všechny soubory v tomto projektu** nebo **všechny soubory v této složce projektu**.</span><span class="sxs-lookup"><span data-stu-id="52f82-125">Other options are **All files in this project** or **All files in this project folder**.</span></span> <span data-ttu-id="52f82-126">Ponechte výchozí výběr, beze změny byste se vyhnout soubory zdrojového kódu, například nasazení.</span><span class="sxs-lookup"><span data-stu-id="52f82-126">By leaving the default selection unchanged you avoid deploying source code files, for example.</span></span> <span data-ttu-id="52f82-127">Toto nastavení je důvod, proč složky obsahující binární soubory systému SQL Server Compact musí být zahrnutý v projektu.</span><span class="sxs-lookup"><span data-stu-id="52f82-127">This setting is the reason why the folders that contain the SQL Server Compact binary files had to be included in the project.</span></span> <span data-ttu-id="52f82-128">Další informace o tomto nastavení najdete v tématu **Proč nejsou všechny soubory ve složce projektu nasazení?** v [technologie ASP.NET webové aplikace projektu nasazení – nejčastější dotazy](https://msdn.microsoft.com/library/ee942158.aspx).</span><span class="sxs-lookup"><span data-stu-id="52f82-128">For more information about this setting, see **Why don't all of the files in my project folder get deployed?** in [ASP.NET Web Application Project Deployment FAQ](https://msdn.microsoft.com/library/ee942158.aspx).</span></span>
- <span data-ttu-id="52f82-129">**Vyloučit generované symboly ladění** zaškrtnuto.</span><span class="sxs-lookup"><span data-stu-id="52f82-129">**Exclude generated debug symbols** is selected.</span></span> <span data-ttu-id="52f82-130">Nesmí být ladění při použití této konfigurace sestavení.</span><span class="sxs-lookup"><span data-stu-id="52f82-130">You won't be debugging when you use this build configuration.</span></span>
- <span data-ttu-id="52f82-131">**Zahrnout všechny databáze, které jsou nakonfigurované v kartě Balení/publikování kódu SQL** zaškrtnuto.</span><span class="sxs-lookup"><span data-stu-id="52f82-131">**Include all databases configured in Package/Publish SQL tab** is selected.</span></span> <span data-ttu-id="52f82-132">Určuje, zda sady Visual Studio nasadí databáze, jakož i soubory.</span><span class="sxs-lookup"><span data-stu-id="52f82-132">Specifies whether Visual Studio will deploy databases as well as files.</span></span> <span data-ttu-id="52f82-133">I když zaškrtnutí políčka popisek pouze zmínky **balení/publikování kódu SQL** kartu, zrušíte zaškrtnutí tohoto políčka by také zakázat nasazení databáze, který je nakonfigurovaný v profilu publikování.</span><span class="sxs-lookup"><span data-stu-id="52f82-133">Although the check box label only mentions the **Package/Publish SQL** tab, clearing this check box would also disable database deployment that is configured in the publish profile.</span></span> <span data-ttu-id="52f82-134">Můžete se být způsobem, který později, tak zaškrtnutí políčka musí zůstat vybrané.</span><span class="sxs-lookup"><span data-stu-id="52f82-134">You will be doing that later, so the check box must remain selected.</span></span> <span data-ttu-id="52f82-135">**Balení/publikování kódu SQL** karta se používá pro starší verze databáze publikování metodu, která nebudete používat v těchto kurzech.</span><span class="sxs-lookup"><span data-stu-id="52f82-135">The **Package/Publish SQL** tab is used for a legacy database publishing method that you won't be using in these tutorials.</span></span>
- <span data-ttu-id="52f82-136">**Nastavení balíčku pro nasazení webových** část se nevztahuje, protože používáte jedním kliknutím publikovat v těchto kurzech.</span><span class="sxs-lookup"><span data-stu-id="52f82-136">The **Web Deployment Package Settings** section does not apply because you're using one-click publish in these tutorials.</span></span>

<span data-ttu-id="52f82-137">Změnit **konfigurace** rozevíracího seznamu pro ladění, pokud chcete zobrazit výchozí nastavení pro sestavení pro ladění.</span><span class="sxs-lookup"><span data-stu-id="52f82-137">Change the **Configuration** drop-down box to Debug to see the default settings for Debug builds.</span></span> <span data-ttu-id="52f82-138">Hodnoty jsou stejné, s výjimkou **Vyloučit generované symboly ladění** je prázdná, takže můžete ladit při nasazování sestavení pro ladění.</span><span class="sxs-lookup"><span data-stu-id="52f82-138">The values are the same, except **Exclude generated debug symbols** is cleared so that you can debug when you deploy a Debug build.</span></span>

## <a name="make-sure-that-the-elmah-folder-gets-deployed"></a><span data-ttu-id="52f82-139">Ujistěte se, že se nasadí Elmah složky</span><span class="sxs-lookup"><span data-stu-id="52f82-139">Make sure that the Elmah folder gets deployed</span></span>

<span data-ttu-id="52f82-140">Jak už jste viděli v předchozím kurzu, [balíček NuGet knihovny Elmah](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) poskytuje funkce pro protokolování a vykazováním chyb.</span><span class="sxs-lookup"><span data-stu-id="52f82-140">As you saw in the previous tutorial, the [Elmah NuGet package](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) provides functionality for error logging and reporting.</span></span> <span data-ttu-id="52f82-141">Aplikace Contoso University Elmah nakonfigurovaný k ukládání podrobnosti o chybě ve složce s názvem *Elmah*:</span><span class="sxs-lookup"><span data-stu-id="52f82-141">In the Contoso University application Elmah has been configured to store error details in a folder named *Elmah*:</span></span>

![Elmah složky](project-properties/_static/image3.png)

<span data-ttu-id="52f82-143">Vyloučení určitých souborů nebo složek z nasazení je běžné požadavky; Dalším příkladem může být složka, která mohou uživatelé odeslat soubory do.</span><span class="sxs-lookup"><span data-stu-id="52f82-143">Excluding specific files or folders from deployment is a common requirement; another example would be a folder that users can upload files to.</span></span> <span data-ttu-id="52f82-144">Nechcete, aby se soubory protokolu nebo nahrát soubory, které byly vytvořeny ve vašem vývojovém prostředí k nasazení do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="52f82-144">You don't want log files or uploaded files that were created in your development environment to be deployed to production.</span></span> <span data-ttu-id="52f82-145">A Pokud nasazujete aktualizace do produkčního prostředí, které nechcete, aby proces nasazení k odstranění souborů, které existují v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="52f82-145">And if you are deploying an update to production you don't want the deployment process to delete files that exist in production.</span></span> <span data-ttu-id="52f82-146">(V závislosti na tom, jak nastavit možnost nasazení, pokud soubor existuje v cílové lokalitě, ale ne zdrojové lokality, když nasazujete, Web Deploy neodstraní z cílového umístění.)</span><span class="sxs-lookup"><span data-stu-id="52f82-146">(Depending on how you set a deployment option, if a file exists in the destination site but not the source site when you deploy, Web Deploy deletes it from the destination.)</span></span>

<span data-ttu-id="52f82-147">Jak už jste viděli dříve v tomto kurzu **položky, které chcete nasadit** možnost **balení/publikování webu** karty nastavená na **pouze soubory potřebné ke spuštění této aplikace**.</span><span class="sxs-lookup"><span data-stu-id="52f82-147">As you saw earlier in this tutorial, the **Items to deploy** option in the **Package/Publish Web** tab is set to **Only Files Needed to run this application**.</span></span> <span data-ttu-id="52f82-148">V důsledku toho soubory protokolů, které jsou vytvořeny pomocí knihovny Elmah ve vývoji nebude nasazena, což je, co byste chtěli.</span><span class="sxs-lookup"><span data-stu-id="52f82-148">As a result, log files that are created by Elmah in development will not be deployed, which is what you want to happen.</span></span> <span data-ttu-id="52f82-149">(Má být nasazen, bylo by nutné zahrnutý v projektu a jejich **akce sestavení** vlastnost musel být nastaveno na **obsahu**.</span><span class="sxs-lookup"><span data-stu-id="52f82-149">(To be deployed, they would have to be included in the project and their **Build Action** property would have to be set to **Content**.</span></span> <span data-ttu-id="52f82-150">Další informace najdete v tématu **Proč nejsou všechny soubory ve složce projektu nasazení?** v [technologie ASP.NET webové aplikace projektu nasazení – nejčastější dotazy](https://msdn.microsoft.com/library/ee942158.aspx)).</span><span class="sxs-lookup"><span data-stu-id="52f82-150">For more information, see **Why don't all of the files in my project folder get deployed?** in [ASP.NET Web Application Project Deployment FAQ](https://msdn.microsoft.com/library/ee942158.aspx)).</span></span> <span data-ttu-id="52f82-151">Ale Webdeploy nebude vytvořte složku v cílové lokalitě pokud existuje alespoň jeden soubor zkopírujte do něj.</span><span class="sxs-lookup"><span data-stu-id="52f82-151">However, Web Deploy will not create a folder in the destination site unless there's at least one file to copy to it.</span></span> <span data-ttu-id="52f82-152">Proto přidáte *.txt* soubor do složky tak, aby fungoval jako zástupný symbol, takže budou zkopírovány složky.</span><span class="sxs-lookup"><span data-stu-id="52f82-152">Therefore, you'll add a *.txt* file to the folder to act as a placeholder so that the folder will be copied.</span></span>

<span data-ttu-id="52f82-153">V **Průzkumníka řešení**, klikněte pravým tlačítkem myši *Elmah* složky, vyberte **přidat novou položku**a vytvořte textový soubor s názvem *Placeholder.txt*.</span><span class="sxs-lookup"><span data-stu-id="52f82-153">In **Solution Explorer**, right-click the *Elmah* folder, select **Add New Item**, and create a text file named *Placeholder.txt*.</span></span> <span data-ttu-id="52f82-154">Vložte následující text do něj: "Toto je zástupný soubor k zajištění, že se nasadí složky".</span><span class="sxs-lookup"><span data-stu-id="52f82-154">Put the following text in it: "This is a placeholder file to ensure that the folder gets deployed."</span></span> <span data-ttu-id="52f82-155">a uložte soubor.</span><span class="sxs-lookup"><span data-stu-id="52f82-155">and save the file.</span></span> <span data-ttu-id="52f82-156">To je všechno musíte udělat, pokud chcete mít jistotu, že sada Visual Studio nasadí tento soubor a složku probíhá, protože **akce sestavení** vlastnost *.txt* souborů je nastavena na **obsahu**ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="52f82-156">That's all you have to do in order to make sure that Visual Studio deploys this file and the folder it's in, because the **Build Action** property of *.txt* files is set to **Content** by default.</span></span>

## <a name="summary"></a><span data-ttu-id="52f82-157">Souhrn</span><span class="sxs-lookup"><span data-stu-id="52f82-157">Summary</span></span>

<span data-ttu-id="52f82-158">Teď jste dokončili všechny kroky nastavení nasazení.</span><span class="sxs-lookup"><span data-stu-id="52f82-158">You have now completed all of the deployment set-up tasks.</span></span> <span data-ttu-id="52f82-159">V dalším kurzu budete nasazení webu společnosti Contoso University do testovacího prostředí a ho vyzkoušeli.</span><span class="sxs-lookup"><span data-stu-id="52f82-159">In the next tutorial, you'll deploy the Contoso University site to the test environment and test it there.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="52f82-160">[Předchozí](web-config-transformations.md)
> [další](deploying-to-iis.md)</span><span class="sxs-lookup"><span data-stu-id="52f82-160">[Previous](web-config-transformations.md)
[Next](deploying-to-iis.md)</span></span>