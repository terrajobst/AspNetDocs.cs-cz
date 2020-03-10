---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení příkazového řádku | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630919"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="581c4-103">Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení z příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="581c4-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>

<span data-ttu-id="581c4-104">tím, že [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="581c4-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="581c4-105">Stáhnout počáteční projekt</span><span class="sxs-lookup"><span data-stu-id="581c4-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="581c4-106">V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="581c4-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="581c4-107">Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="581c4-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="581c4-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="581c4-108">Overview</span></span>

<span data-ttu-id="581c4-109">V tomto kurzu se dozvíte, jak vyvolat kanál publikování webu sady Visual Studio z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="581c4-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="581c4-110">To je užitečné ve scénářích, kde chcete [automatizovat proces nasazení](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) místo ručního provedení v aplikaci Visual Studio, obvykle pomocí [systému správy verzí zdrojového kódu](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span><span class="sxs-lookup"><span data-stu-id="581c4-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="581c4-111">Provedení změny nasazení</span><span class="sxs-lookup"><span data-stu-id="581c4-111">Make a change to deploy</span></span>

<span data-ttu-id="581c4-112">V současné době stránka o produktu zobrazuje kód šablony.</span><span class="sxs-lookup"><span data-stu-id="581c4-112">Currently the About page displays the template code.</span></span>

![Stránka s kódem šablony](command-line-deployment/_static/image1.png)

<span data-ttu-id="581c4-114">Nahradíte ho kódem, který zobrazuje souhrn registrace studenta.</span><span class="sxs-lookup"><span data-stu-id="581c4-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="581c4-115">Otevřete stránku *About. aspx* , odstraňte všechny značky uvnitř elementu `MainContent` `Content` a vložte následující kód do svého umístění:</span><span class="sxs-lookup"><span data-stu-id="581c4-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="581c4-116">Spusťte projekt a vyberte stránku **o produktu** .</span><span class="sxs-lookup"><span data-stu-id="581c4-116">Run the project and select the **About** page.</span></span>

![O stránce](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="581c4-118">Nasazení na test pomocí příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="581c4-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="581c4-119">Nebudete nasazovat jinou změnu databáze, takže zakážete nasazení databáze dbDacFx pro databázi ASPNET-ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="581c4-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="581c4-120">Otevřete Průvodce **publikováním webu** a v každém ze tří profilů publikování zrušte zaškrtnutí políčka **aktualizovat databázi** na kartě **Nastavení** .</span><span class="sxs-lookup"><span data-stu-id="581c4-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="581c4-121">Na úvodní stránce Windows 8 vyhledejte **Developer Command Prompt pro VS2012**.</span><span class="sxs-lookup"><span data-stu-id="581c4-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="581c4-122">Klikněte pravým tlačítkem na ikonu **Developer Command Prompt pro VS2012** a klikněte na **Spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="581c4-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="581c4-123">Na příkazovém řádku zadejte následující příkaz, který nahradí cestu k souboru řešení cestou k souboru řešení:</span><span class="sxs-lookup"><span data-stu-id="581c4-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="581c4-124">Nástroj MSBuild sestaví řešení a nasadí ho do testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="581c4-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![Výstup příkazového řádku](command-line-deployment/_static/image3.png)

<span data-ttu-id="581c4-126">Otevřete prohlížeč a přejděte na `http://localhost/ContosoUniversity`a kliknutím na stránku **o** ověřte, že nasazení proběhlo úspěšně.</span><span class="sxs-lookup"><span data-stu-id="581c4-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="581c4-127">Pokud jste nevytvořili žádné studenty v testu, zobrazí se v záhlaví **Statistika těla studenta** prázdná stránka.</span><span class="sxs-lookup"><span data-stu-id="581c4-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="581c4-128">Přejděte na stránku **Students** , klikněte na **Přidat studenta**a přidejte nějaké studenty a pak se vraťte na stránku **o produktu** a podívejte se na téma o statistice studenta.</span><span class="sxs-lookup"><span data-stu-id="581c4-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![O stránce v testovacím prostředí](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="581c4-130">Možnosti příkazového řádku pro klávesu</span><span class="sxs-lookup"><span data-stu-id="581c4-130">Key command line options</span></span>

<span data-ttu-id="581c4-131">Příkaz, který jste zadali, předali cestu k souboru řešení a dvěma vlastnostem na MSBuild:</span><span class="sxs-lookup"><span data-stu-id="581c4-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="581c4-132">Nasazení řešení vs. nasazení jednotlivých projektů</span><span class="sxs-lookup"><span data-stu-id="581c4-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="581c4-133">Zadáním souboru řešení dojde k sestavení všech projektů v tomto řešení.</span><span class="sxs-lookup"><span data-stu-id="581c4-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="581c4-134">Pokud máte v řešení více webových projektů, platí následující chování nástroje MSBuild:</span><span class="sxs-lookup"><span data-stu-id="581c4-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="581c4-135">Vlastnosti, které zadáte v příkazovém řádku, jsou předány do každého projektu.</span><span class="sxs-lookup"><span data-stu-id="581c4-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="581c4-136">Proto každý webový projekt musí mít profil publikování s názvem, který zadáte.</span><span class="sxs-lookup"><span data-stu-id="581c4-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="581c4-137">Zadáte-li `/p:PublishProfile=Test`, musí mít každý webový projekt profil publikování s názvem *test*.</span><span class="sxs-lookup"><span data-stu-id="581c4-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="581c4-138">Jeden projekt může být úspěšně publikován, i když jiný není sestaven.</span><span class="sxs-lookup"><span data-stu-id="581c4-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="581c4-139">Další informace naleznete v tématu StackOverflow vlákno [MSBuild se nezdařila se dvěma balíčky](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span><span class="sxs-lookup"><span data-stu-id="581c4-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="581c4-140">Pokud zadáte samostatný projekt namísto řešení, je nutné přidat parametr, který určuje verzi sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="581c4-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="581c4-141">Pokud používáte Visual Studio 2012, příkazový řádek by byl podobný následujícímu příkladu:</span><span class="sxs-lookup"><span data-stu-id="581c4-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="581c4-142">Číslo verze sady Visual Studio 2010 je 10,0.</span><span class="sxs-lookup"><span data-stu-id="581c4-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="581c4-143">Další informace najdete v tématu [Kompatibilita projektů v aplikaci Visual Studio a VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) na blogu Sayed Hashimi.</span><span class="sxs-lookup"><span data-stu-id="581c4-143">For more information, see [Visual Studio project compatibility and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="581c4-144">Zadání profilu publikování</span><span class="sxs-lookup"><span data-stu-id="581c4-144">Specifying the publish profile</span></span>

<span data-ttu-id="581c4-145">Můžete zadat profil publikování podle názvu nebo úplnou cestou k souboru *. pubxml* , jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="581c4-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="581c4-146">Metody publikování na webu podporované pro publikování z příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="581c4-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="581c4-147">Pro publikování na příkazovém řádku jsou podporované tři metody publikování:</span><span class="sxs-lookup"><span data-stu-id="581c4-147">Three publish methods are supported for command line publishing:</span></span>

- <span data-ttu-id="581c4-148">`MSDeploy` – publikování pomocí Nasazení webu.</span><span class="sxs-lookup"><span data-stu-id="581c4-148">`MSDeploy` - Publish by using Web Deploy.</span></span>
- <span data-ttu-id="581c4-149">`Package` – publikování vytvořením balíčku Nasazení webu.</span><span class="sxs-lookup"><span data-stu-id="581c4-149">`Package` - Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="581c4-150">Balíček je nutné nainstalovat samostatně z příkazu MSBuild, který ho vytvoří.</span><span class="sxs-lookup"><span data-stu-id="581c4-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- <span data-ttu-id="581c4-151">`FileSystem` – publikování kopírováním souborů do zadané složky.</span><span class="sxs-lookup"><span data-stu-id="581c4-151">`FileSystem` - Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="581c4-152">Zadání konfigurace sestavení a platformy</span><span class="sxs-lookup"><span data-stu-id="581c4-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="581c4-153">Konfigurace sestavení a platforma musí být nastavená v sadě Visual Studio nebo na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="581c4-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="581c4-154">Profily publikování zahrnují vlastnosti, které jsou pojmenovány `LastUsedBuildConfiguration` a `LastUsedPlatform`, ale tyto vlastnosti nelze nastavit, aby bylo možné určit, jak je projekt sestaven.</span><span class="sxs-lookup"><span data-stu-id="581c4-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="581c4-155">Další informace najdete v tématu [MSBuild: jak nastavit vlastnost konfigurace](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) na blogu Sayed Hashimi.</span><span class="sxs-lookup"><span data-stu-id="581c4-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="581c4-156">Nasazení do přípravného prostředí</span><span class="sxs-lookup"><span data-stu-id="581c4-156">Deploy to staging</span></span>

<span data-ttu-id="581c4-157">K nasazení do Azure je nutné přidat heslo do příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="581c4-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="581c4-158">Pokud jste heslo uložili v profilu publikování v aplikaci Visual Studio, bylo uloženo v šifrované podobě v souboru *. pubxml. User* .</span><span class="sxs-lookup"><span data-stu-id="581c4-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="581c4-159">Tento soubor není nástrojem MSBuild k dispozici při nasazení příkazového řádku, takže je nutné předat heslo v parametru příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="581c4-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="581c4-160">Zkopírujte heslo, které potřebujete, ze souboru *. publishsettings* , který jste si stáhli dříve pro pracovní web.</span><span class="sxs-lookup"><span data-stu-id="581c4-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="581c4-161">Heslo je hodnota atributu `userPWD` prvku Nasazení webu `publishProfile`.</span><span class="sxs-lookup"><span data-stu-id="581c4-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![Nasazení webu heslo](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="581c4-163">Na úvodní stránce Windows 8 vyhledejte **Developer Command Prompt pro VS2012**a kliknutím na ikonu otevřete příkazový řádek.</span><span class="sxs-lookup"><span data-stu-id="581c4-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="581c4-164">(Nemusíte ho otevírat jako správce, protože neprovádíte nasazení do služby IIS v místním počítači.)</span><span class="sxs-lookup"><span data-stu-id="581c4-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="581c4-165">Na příkazovém řádku zadejte následující příkaz, který nahradí cestu k souboru řešení cestou k souboru řešení a heslo s vaším heslem:</span><span class="sxs-lookup"><span data-stu-id="581c4-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="581c4-166">Všimněte si, že tento příkazový řádek obsahuje další parametr: `/p:AllowUntrustedCertificate=true`.</span><span class="sxs-lookup"><span data-stu-id="581c4-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="581c4-167">Při psaní tohoto kurzu musí být vlastnost `AllowUntrustedCertificate` nastavena při publikování do Azure z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="581c4-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="581c4-168">Po vydání opravy pro tuto chybu nebudete potřebovat parametr.</span><span class="sxs-lookup"><span data-stu-id="581c4-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="581c4-169">Otevřete prohlížeč a přejděte na adresu URL vašeho přípravného webu a kliknutím na stránku **o** ověřte, že nasazení proběhlo úspěšně.</span><span class="sxs-lookup"><span data-stu-id="581c4-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="581c4-170">Jak jste viděli dříve pro testovací prostředí, možná budete muset vytvořit nějaké studenty, aby viděli statistiku na stránce **o produktu** .</span><span class="sxs-lookup"><span data-stu-id="581c4-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="581c4-171">Nasazení do produkčního prostředí</span><span class="sxs-lookup"><span data-stu-id="581c4-171">Deploy to production</span></span>

<span data-ttu-id="581c4-172">Proces pro nasazení do produkčního prostředí je podobný procesu pro přípravu.</span><span class="sxs-lookup"><span data-stu-id="581c4-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="581c4-173">Zkopírujte heslo, které potřebujete, ze souboru *. publishsettings* , který jste si stáhli dříve pro produkční Web.</span><span class="sxs-lookup"><span data-stu-id="581c4-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="581c4-174">Otevřete **Developer Command Prompt pro VS2012**.</span><span class="sxs-lookup"><span data-stu-id="581c4-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="581c4-175">Na příkazovém řádku zadejte následující příkaz, který nahradí cestu k souboru řešení cestou k souboru řešení a heslo s vaším heslem:</span><span class="sxs-lookup"><span data-stu-id="581c4-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="581c4-176">V případě skutečného produkčního webu, pokud došlo ke změně databáze, byste obvykle zkopírovali *aplikaci\_offline souboru. htm* do lokality před nasazením a po úspěšném nasazení ho odstraníte.</span><span class="sxs-lookup"><span data-stu-id="581c4-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="581c4-177">Otevřete prohlížeč a přejděte na adresu URL vašeho přípravného webu a kliknutím na stránku **o** ověřte, že nasazení proběhlo úspěšně.</span><span class="sxs-lookup"><span data-stu-id="581c4-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="581c4-178">Souhrn</span><span class="sxs-lookup"><span data-stu-id="581c4-178">Summary</span></span>

<span data-ttu-id="581c4-179">Nyní jste nasadili aktualizaci aplikace pomocí příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="581c4-179">You have now deployed an application update by using the command line.</span></span>

![O stránce v testovacím prostředí](command-line-deployment/_static/image6.png)

<span data-ttu-id="581c4-181">V dalším kurzu se zobrazí příklad rozšiřování kanálu publikování na webu.</span><span class="sxs-lookup"><span data-stu-id="581c4-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="581c4-182">V tomto příkladu se dozvíte, jak nasadit soubory, které nejsou zahrnuty v projektu.</span><span class="sxs-lookup"><span data-stu-id="581c4-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="581c4-183">[Předchozí](deploying-a-database-update.md)
> [Další](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="581c4-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
