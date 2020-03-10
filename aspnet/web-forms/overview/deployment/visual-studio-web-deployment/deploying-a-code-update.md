---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení aktualizace kódu | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567401"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="e35b7-103">Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení aktualizace kódu</span><span class="sxs-lookup"><span data-stu-id="e35b7-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>

<span data-ttu-id="e35b7-104">tím, že [Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e35b7-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="e35b7-105">Stáhnout počáteční projekt</span><span class="sxs-lookup"><span data-stu-id="e35b7-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="e35b7-106">V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="e35b7-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="e35b7-107">Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e35b7-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="e35b7-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="e35b7-108">Overview</span></span>

<span data-ttu-id="e35b7-109">Po počátečním nasazení bude vaše práce s údržbou a vývojem webu pokračovat a ještě dlouho budete chtít nasadit aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="e35b7-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="e35b7-110">Tento kurz vás provede procesem nasazení aktualizace kódu vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="e35b7-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="e35b7-111">Aktualizace, kterou implementujete a nasadíte v tomto kurzu, nezahrnuje změnu databáze. v dalším kurzu se dozvíte, jaké jsou různé informace o nasazení změny databáze.</span><span class="sxs-lookup"><span data-stu-id="e35b7-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="e35b7-112">Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e35b7-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="e35b7-113">Provedení změny kódu</span><span class="sxs-lookup"><span data-stu-id="e35b7-113">Make a code change</span></span>

<span data-ttu-id="e35b7-114">Jako jednoduchý příklad aktualizace aplikace přidáváte na stránku **instruktoři** seznam kurzů, které probral vybraný instruktor.</span><span class="sxs-lookup"><span data-stu-id="e35b7-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="e35b7-115">Pokud spouštíte stránku **instruktory** , všimnete si, že v mřížce jsou **vybrané** odkazy, ale nedělají nic jiného, než když se pozadí řádku změní na šedé.</span><span class="sxs-lookup"><span data-stu-id="e35b7-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![Stránka instruktoři s výběrem](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="e35b7-117">Nyní přidáte kód, který se spustí, když se klikne na odkaz **Select** , a zobrazí se seznam kurzů, které prochází vybraným instruktorem.</span><span class="sxs-lookup"><span data-stu-id="e35b7-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="e35b7-118">V *instruktors. aspx*přidejte následující kód hned za ovládací prvek **ErrorMessageLabel** `Label`:</span><span class="sxs-lookup"><span data-stu-id="e35b7-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="e35b7-119">Spusťte stránku a vyberte instruktor.</span><span class="sxs-lookup"><span data-stu-id="e35b7-119">Run the page and select an instructor.</span></span> <span data-ttu-id="e35b7-120">Zobrazí se seznam výukových kurzů, které tento instruktor projedná.</span><span class="sxs-lookup"><span data-stu-id="e35b7-120">You see a list of courses taught by that instructor.</span></span>

    ![Stránka instruktorů s výukou kurzů](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="e35b7-122">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="e35b7-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="e35b7-123">Nasazení aktualizace kódu do testovacího prostředí</span><span class="sxs-lookup"><span data-stu-id="e35b7-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="e35b7-124">Než budete moct použít svoje profily publikování k nasazení na testování, přípravu a produkční prostředí, musíte změnit možnosti publikování databáze.</span><span class="sxs-lookup"><span data-stu-id="e35b7-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="e35b7-125">Už nemusíte spouštět skripty pro udělení a nasazování dat pro databázi členství.</span><span class="sxs-lookup"><span data-stu-id="e35b7-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="e35b7-126">Otevřete Průvodce **publikováním webu** kliknutím pravým tlačítkem myši na projekt ContosoUniversity a kliknutím na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="e35b7-127">V rozevíracím seznamu **profil** klikněte na profil **testu** .</span><span class="sxs-lookup"><span data-stu-id="e35b7-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="e35b7-128">Klikněte na kartu **Nastavení**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="e35b7-129">V části **DefaultConnection** v části **databáze** zrušte zaškrtnutí políčka **aktualizovat databázi** .</span><span class="sxs-lookup"><span data-stu-id="e35b7-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="e35b7-130">Klikněte na kartu **profil** a potom v rozevíracím seznamu **profil** klikněte na **pracovní** profil.</span><span class="sxs-lookup"><span data-stu-id="e35b7-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="e35b7-131">Když se zobrazí dotaz, zda chcete uložit změny provedené v profilu **testu** , klikněte na tlačítko **Ano**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="e35b7-132">Udělejte stejnou změnu v pracovním profilu.</span><span class="sxs-lookup"><span data-stu-id="e35b7-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="e35b7-133">Zopakováním tohoto postupu provedete stejnou změnu v produkčním profilu.</span><span class="sxs-lookup"><span data-stu-id="e35b7-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="e35b7-134">Zavřete průvodce **publikováním webu** .</span><span class="sxs-lookup"><span data-stu-id="e35b7-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="e35b7-135">Nasazení do testovacího prostředí je teď jednoduchou záležitostí opětovného spuštění publikování jedním kliknutím.</span><span class="sxs-lookup"><span data-stu-id="e35b7-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="e35b7-136">Chcete-li tento proces urychlit, můžete použít panel nástrojů pro **publikování webu jedním kliknutím** .</span><span class="sxs-lookup"><span data-stu-id="e35b7-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="e35b7-137">V nabídce **zobrazení** zvolte **panely nástrojů** a pak vyberte **možnost publikovat na webu jedním kliknutím**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="e35b7-139">V **Průzkumník řešení**vyberte projekt ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="e35b7-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="e35b7-140">panel nástrojů pro **publikování webu jedním kliknutím** vyberte profil publikování **testu** a pak klikněte na **Publikovat web** (ikona se šipkami ukazující vlevo a vpravo).</span><span class="sxs-lookup"><span data-stu-id="e35b7-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="e35b7-142">Visual Studio nasadí aktualizovanou aplikaci a prohlížeč se automaticky otevře na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="e35b7-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="e35b7-143">Spusťte stránku instruktoři a vyberte instruktora, abyste ověřili, že byla aktualizace úspěšně nasazena.</span><span class="sxs-lookup"><span data-stu-id="e35b7-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="e35b7-144">Obvykle byste také provedli regresní testování (to znamená otestovat zbytek lokality, abyste se ujistili, že nová změna nepřerušila všechny stávající funkce).</span><span class="sxs-lookup"><span data-stu-id="e35b7-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="e35b7-145">Pro tento kurz ale tento krok přeskočíte a pokračujte v nasazení aktualizace do pracovních a produkčních prostředí.</span><span class="sxs-lookup"><span data-stu-id="e35b7-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="e35b7-146">Když znovu nasadíte, Nasazení webu automaticky určí, které soubory se změnily, a na server se zkopírují jenom změněné soubory.</span><span class="sxs-lookup"><span data-stu-id="e35b7-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="e35b7-147">Ve výchozím nastavení Nasazení webu používá datum poslední změny souborů k určení, které z nich se změnily.</span><span class="sxs-lookup"><span data-stu-id="e35b7-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="e35b7-148">Některé systémy správy zdrojového kódu mění data souborů i v případě, že neměníte obsah souboru.</span><span class="sxs-lookup"><span data-stu-id="e35b7-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="e35b7-149">V takovém případě můžete chtít nakonfigurovat Nasazení webu, aby používaly kontrolní součty souborů k určení, které soubory se změnily.</span><span class="sxs-lookup"><span data-stu-id="e35b7-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="e35b7-150">Další informace najdete v tématu [Proč se všechny moje soubory znovu nasazují, i když jsem nezměnili?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) v nejčastějších dotazech k nasazení ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e35b7-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="e35b7-151">Při nasazení převést aplikaci do offline režimu</span><span class="sxs-lookup"><span data-stu-id="e35b7-151">Take the application offline during deployment</span></span>

<span data-ttu-id="e35b7-152">Změna, kterou právě nasazujete, je jednoduchá změna na jednu stránku.</span><span class="sxs-lookup"><span data-stu-id="e35b7-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="e35b7-153">Někdy ale nasadíte větší změny nebo nasadíte změny kódu i databáze a lokalita se může chovat nesprávně, pokud uživatel požádá o stránku před dokončením nasazení.</span><span class="sxs-lookup"><span data-stu-id="e35b7-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="e35b7-154">Pokud chcete zabránit uživatelům v přístupu k webu, když probíhá nasazení, můžete použít *aplikaci\_offline souboru. htm* .</span><span class="sxs-lookup"><span data-stu-id="e35b7-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="e35b7-155">Když umístíte soubor s názvem *app\_v režimu offline. htm* do kořenové složky vaší aplikace, služba IIS automaticky zobrazí tento soubor místo spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="e35b7-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="e35b7-156">Pokud tedy chcete během nasazení zabránit přístupu, vložte *aplikaci\_do režimu offline. htm* v kořenové složce, spusťte proces nasazení a po úspěšném nasazení odeberte *aplikaci\_offline. htm* .</span><span class="sxs-lookup"><span data-stu-id="e35b7-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="e35b7-157">Nasazení webu můžete nakonfigurovat tak, aby při zahájení nasazování automaticky umístila výchozí *aplikaci\_offline soubor. htm* na server, a po dokončení ho odebere.</span><span class="sxs-lookup"><span data-stu-id="e35b7-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="e35b7-158">Chcete-li provést vše, co musíte udělat, přidejte do souboru publikačního profilu (. pubxml) následující element XML:</span><span class="sxs-lookup"><span data-stu-id="e35b7-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="e35b7-159">V tomto kurzu se dozvíte, jak vytvořit a použít vlastní *aplikaci\_offline souboru. htm* .</span><span class="sxs-lookup"><span data-stu-id="e35b7-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="e35b7-160">Použití *aplikace\_offline. htm* v pracovní lokalitě není vyžadováno, protože nemáte přístup k pracovnímu webu.</span><span class="sxs-lookup"><span data-stu-id="e35b7-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="e35b7-161">Je ale vhodné použít fázování k otestování všech způsobů, jak plánujete nasazení v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="e35b7-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-app_offlinehtm"></a><span data-ttu-id="e35b7-162">Vytvoření aplikace\_offline. htm</span><span class="sxs-lookup"><span data-stu-id="e35b7-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="e35b7-163">V **Průzkumník řešení**klikněte pravým tlačítkem myši na řešení, klikněte na tlačítko **Přidat**a poté klikněte na položku **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="e35b7-164">Vytvořte **stránku HTML** s názvem *App\_offline. htm* (odstraňte poslední "l" v rozšíření *. html* , které Visual Studio vytvoří ve výchozím nastavení).</span><span class="sxs-lookup"><span data-stu-id="e35b7-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="e35b7-165">Nahraďte kód šablony následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="e35b7-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="e35b7-166">Uložte soubor a zavřete ho.</span><span class="sxs-lookup"><span data-stu-id="e35b7-166">Save and close the file.</span></span>

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="e35b7-167">Zkopírujte aplikaci\_offline. htm do kořenové složky webu.</span><span class="sxs-lookup"><span data-stu-id="e35b7-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="e35b7-168">K kopírování souborů na web můžete použít libovolný nástroj FTP.</span><span class="sxs-lookup"><span data-stu-id="e35b7-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="e35b7-169">[FileZilly](http://filezilla-project.org/) je oblíbený nástroj FTP, který se zobrazuje ve snímkůch obrazovky.</span><span class="sxs-lookup"><span data-stu-id="e35b7-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="e35b7-170">Chcete-li použít nástroj FTP, budete potřebovat tři věci: adresu URL serveru FTP, uživatelské jméno a heslo.</span><span class="sxs-lookup"><span data-stu-id="e35b7-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="e35b7-171">Adresa URL se zobrazí na stránce řídicí panel webu v Azure Portál pro správu a uživatelské jméno a heslo pro FTP najdete v souboru *. publishsettings* , který jste si stáhli dříve.</span><span class="sxs-lookup"><span data-stu-id="e35b7-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="e35b7-172">Následující kroky ukazují, jak tyto hodnoty získat.</span><span class="sxs-lookup"><span data-stu-id="e35b7-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="e35b7-173">V Portál pro správu Azure klikněte na kartu **webové servery** a potom klikněte na pracovní web.</span><span class="sxs-lookup"><span data-stu-id="e35b7-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="e35b7-174">Na stránce **řídicí panel** přejděte dolů a vyhledejte název hostitele FTP v části **rychlý přehled** .</span><span class="sxs-lookup"><span data-stu-id="e35b7-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![Název hostitele FTP](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="e35b7-176">V programu Poznámkový blok nebo jiném textovém editoru otevřete soubor staging *. publishsettings* .</span><span class="sxs-lookup"><span data-stu-id="e35b7-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="e35b7-177">Vyhledejte prvek `publishProfile` pro profil FTP.</span><span class="sxs-lookup"><span data-stu-id="e35b7-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="e35b7-178">Zkopírujte hodnoty `userName` a `userPWD`.</span><span class="sxs-lookup"><span data-stu-id="e35b7-178">Copy the `userName` and `userPWD` values.</span></span>

    ![Přihlašovací údaje FTP](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="e35b7-180">Otevřete nástroj FTP a přihlaste se k adrese URL serveru FTP.</span><span class="sxs-lookup"><span data-stu-id="e35b7-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="e35b7-181">Zkopírujte *aplikaci\_offline. htm* ze složky řešení do složky */site/wwwroot* v přípravném webu.</span><span class="sxs-lookup"><span data-stu-id="e35b7-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![Kopírovat app_offline](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="e35b7-183">Přejděte na adresu URL vašeho pracovního webu.</span><span class="sxs-lookup"><span data-stu-id="e35b7-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="e35b7-184">Uvidíte, že se teď místo domovské stránky zobrazuje stránka *aplikace\_offline. htm* .</span><span class="sxs-lookup"><span data-stu-id="e35b7-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![app_offline. htm v okně prohlížeče](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="e35b7-186">Nyní jste připraveni na nasazení do přípravy.</span><span class="sxs-lookup"><span data-stu-id="e35b7-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="e35b7-187">Nasazení aktualizace kódu do pracovního a produkčního prostředí</span><span class="sxs-lookup"><span data-stu-id="e35b7-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="e35b7-188">Na panelu nástrojů **publikování webu jedním kliknutím** vyberte profil pro **přípravu** a pak klikněte na **Publikovat web**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="e35b7-189">Visual Studio nasadí aktualizovanou aplikaci a otevře prohlížeč na domovské stránce webu.</span><span class="sxs-lookup"><span data-stu-id="e35b7-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="e35b7-190">Zobrazí se soubor *\_offline. htm aplikace* .</span><span class="sxs-lookup"><span data-stu-id="e35b7-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="e35b7-191">Než budete moct otestovat ověření úspěšného nasazení, musíte *aplikaci odebrat\_offline souboru. htm* .</span><span class="sxs-lookup"><span data-stu-id="e35b7-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="e35b7-192">Vraťte se do nástroje FTP a odstraňte **aplikaci\_offline. htm** z přípravného webu.</span><span class="sxs-lookup"><span data-stu-id="e35b7-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="e35b7-193">V prohlížeči otevřete stránku instruktoři v přípravném webu a vyberte instruktora, abyste ověřili, že byla aktualizace úspěšně nasazena.</span><span class="sxs-lookup"><span data-stu-id="e35b7-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="e35b7-194">Pro produkční prostředí použijte stejný postup jako při přípravě.</span><span class="sxs-lookup"><span data-stu-id="e35b7-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="e35b7-195">Kontrola změn a nasazení určitých souborů</span><span class="sxs-lookup"><span data-stu-id="e35b7-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="e35b7-196">Visual Studio 2012 také umožňuje nasazovat jednotlivé soubory.</span><span class="sxs-lookup"><span data-stu-id="e35b7-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="e35b7-197">Pro vybraný soubor můžete zobrazit rozdíly mezi místní a nasazenou verzí, nasadit soubor do cílového prostředí nebo zkopírovat soubor z cílového prostředí do místního projektu.</span><span class="sxs-lookup"><span data-stu-id="e35b7-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="e35b7-198">V této části kurzu zjistíte, jak tyto funkce používat.</span><span class="sxs-lookup"><span data-stu-id="e35b7-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="e35b7-199">Provedení změny nasazení</span><span class="sxs-lookup"><span data-stu-id="e35b7-199">Make a change to deploy</span></span>

1. <span data-ttu-id="e35b7-200">Otevřete *Content/Web. CSS*a najděte blok značky `body`.</span><span class="sxs-lookup"><span data-stu-id="e35b7-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="e35b7-201">Změňte hodnotu `background-color` z `#fff` na `darkblue`.</span><span class="sxs-lookup"><span data-stu-id="e35b7-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="e35b7-202">Zobrazení změny v okně Publikovat náhled</span><span class="sxs-lookup"><span data-stu-id="e35b7-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="e35b7-203">Když použijete průvodce **Publikovat web** k publikování projektu, můžete zjistit, jaké změny budou publikovány Poklikáním na soubor v okně **náhledu** .</span><span class="sxs-lookup"><span data-stu-id="e35b7-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="e35b7-204">Klikněte pravým tlačítkem na projekt ContosoUniversity a klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="e35b7-205">V rozevíracím seznamu **profil** vyberte profil publikování **testu** .</span><span class="sxs-lookup"><span data-stu-id="e35b7-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="e35b7-206">Klikněte na **Náhled**a pak na **Spustit náhled**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="e35b7-207">V podokně **náhledu** poklikejte na **site. CSS**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![Poklikejte na web. CSS.](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="e35b7-209">V dialogovém okně **Náhled změn** se zobrazí náhled změn, které budou nasazeny.</span><span class="sxs-lookup"><span data-stu-id="e35b7-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![Zobrazit náhled změn v site. CSS](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="e35b7-211">Pokud dvakrát kliknete na soubor *Web. config* , zobrazí dialogové okno **Náhled změn** efekt transformací konfigurace sestavení a publikování profilů.</span><span class="sxs-lookup"><span data-stu-id="e35b7-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="e35b7-212">V tomto okamžiku jste neudělali nic, co by mohlo způsobit změnu souboru *Web. config* na serveru, takže očekáváte, že se nezobrazí žádné změny.</span><span class="sxs-lookup"><span data-stu-id="e35b7-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="e35b7-213">Okno **Náhled změn** ale nesprávně zobrazuje dvě změny.</span><span class="sxs-lookup"><span data-stu-id="e35b7-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="e35b7-214">Vypadá to, že se odeberou dva prvky XML.</span><span class="sxs-lookup"><span data-stu-id="e35b7-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="e35b7-215">Tyto prvky jsou přidány procesem publikování, když vyberete možnost **spustit migrace Code First při spuštění aplikace** pro třídu kontextu Code First.</span><span class="sxs-lookup"><span data-stu-id="e35b7-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="e35b7-216">Porovnání je provedeno před tím, než proces publikování přidá tyto prvky, takže vypadá, že jsou odebírány, i když nebudou odebrány.</span><span class="sxs-lookup"><span data-stu-id="e35b7-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="e35b7-217">Tato chyba bude opravena v budoucí verzi.</span><span class="sxs-lookup"><span data-stu-id="e35b7-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="e35b7-218">Klikněte na **Zavřít**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-218">Click **Close**.</span></span>
6. <span data-ttu-id="e35b7-219">Klikněte na **Publikovat**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-219">Click **Publish**.</span></span>
7. <span data-ttu-id="e35b7-220">Po otevření prohlížeče na domovské stránce testovacího webu stiskněte klávesy CTRL + F5, čímž se zobrazí efekt změny šablony stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="e35b7-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![Účinek změny šablony stylů CSS](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="e35b7-222">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="e35b7-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="e35b7-223">Publikovat konkrétní soubory z Průzkumník řešení</span><span class="sxs-lookup"><span data-stu-id="e35b7-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="e35b7-224">Předpokládejme, že se vám nelíbí modré pozadí a chcete se vrátit k původní barvě.</span><span class="sxs-lookup"><span data-stu-id="e35b7-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="e35b7-225">V této části obnovíte původní nastavení publikováním konkrétního souboru přímo z **Průzkumník řešení**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="e35b7-226">Otevřete *Content/Web. CSS* a obnovte nastavení `background-color` pro `#fff`.</span><span class="sxs-lookup"><span data-stu-id="e35b7-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="e35b7-227">V **Průzkumník řešení**klikněte pravým tlačítkem myši na soubor *Content/Web. CSS* .</span><span class="sxs-lookup"><span data-stu-id="e35b7-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="e35b7-228">Místní nabídka obsahuje tři možnosti publikování.</span><span class="sxs-lookup"><span data-stu-id="e35b7-228">The context menu shows three publish options.</span></span>

    ![Publikování možností z Průzkumník řešení](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="e35b7-230">Klikněte na **Náhled změn v site. CSS**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="e35b7-231">Otevře se okno, ve kterém se zobrazí rozdíly mezi místním souborem a jeho verzí v cílovém prostředí.</span><span class="sxs-lookup"><span data-stu-id="e35b7-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-Content/Site.css](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="e35b7-233">V **Průzkumník řešení**klikněte znovu pravým tlačítkem na **site. CSS** a pak klikněte na **Publikovat web. CSS**.</span><span class="sxs-lookup"><span data-stu-id="e35b7-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="e35b7-234">V okně **aktivity publikování na webu** se zobrazí, že soubor byl publikován.</span><span class="sxs-lookup"><span data-stu-id="e35b7-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![Okno aktivity publikování na webu](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="e35b7-236">Otevřete prohlížeč na adrese URL `http://localhost/contosouniversity` a potom stisknutím kombinace kláves CTRL + F5 zobrazte efekt změny šablony stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="e35b7-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![Domovská stránka s normální šablonou stylů CSS](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="e35b7-238">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="e35b7-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="e35b7-239">Souhrn</span><span class="sxs-lookup"><span data-stu-id="e35b7-239">Summary</span></span>

<span data-ttu-id="e35b7-240">Nyní jste viděli několik způsobů, jak nasadit aktualizaci aplikace, která nezahrnuje změnu databáze a jste viděli, jak zobrazit náhled změn, abyste ověřili, jestli se má aktualizovat, a to, co očekáváte.</span><span class="sxs-lookup"><span data-stu-id="e35b7-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="e35b7-241">Stránka instruktoři má teď oddíl **výukových kurzů** .</span><span class="sxs-lookup"><span data-stu-id="e35b7-241">The Instructors page now has a **Courses Taught** section.</span></span>

![Stránka instruktorů s výukou kurzů](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="e35b7-243">V dalším kurzu se dozvíte, jak nasadit změnu databáze: přidáte pole DatumNarození do databáze a na stránku instruktoři.</span><span class="sxs-lookup"><span data-stu-id="e35b7-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e35b7-244">[Předchozí](deploying-to-production.md)
> [Další](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="e35b7-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
