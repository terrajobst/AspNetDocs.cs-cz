---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Používání webového rozhraní API 2 s Entity Framework 6 | Microsoft Docs
author: MikeWasson
description: V tomto kurzu se naučíte základy vytváření webových aplikací pomocí back-endu webového rozhraní API ASP.NET. Tento kurz používá pro stanovení dat Entity Framework 6...
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622477"
---
# <a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="068cd-104">Použití webového rozhraní API 2 se sadou Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="068cd-104">Using Web API 2 with Entity Framework 6</span></span>

[<span data-ttu-id="068cd-105">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="068cd-105">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="068cd-106">V tomto kurzu se naučíte základy vytváření webových aplikací pomocí back-endu ASP.NET webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="068cd-106">This tutorial teaches you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="068cd-107">Kurz používá pro datovou vrstvu Entity Framework 6 a vyseknutí. js pro aplikaci JavaScriptu na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="068cd-107">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="068cd-108">Tento kurz také ukazuje, jak nasadit aplikaci do Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="068cd-108">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="068cd-109">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="068cd-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="068cd-110">Webové rozhraní API 2,1</span><span class="sxs-lookup"><span data-stu-id="068cd-110">Web API 2.1</span></span>
> - <span data-ttu-id="068cd-111">Visual Studio 2017 ( [tady si můžete](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)stáhnout visual Studio 2017)</span><span class="sxs-lookup"><span data-stu-id="068cd-111">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="068cd-112">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="068cd-112">Entity Framework 6</span></span>
> - <span data-ttu-id="068cd-113">.NET 4.7</span><span class="sxs-lookup"><span data-stu-id="068cd-113">.NET 4.7</span></span>
> - <span data-ttu-id="068cd-114">[Vyseknutí. js](http://knockoutjs.com/) 3,1</span><span class="sxs-lookup"><span data-stu-id="068cd-114">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>

<span data-ttu-id="068cd-115">V tomto kurzu se používá webové rozhraní API 2 ASP.NET s Entity Framework 6 k vytvoření webové aplikace, která pracuje s back-end databází.</span><span class="sxs-lookup"><span data-stu-id="068cd-115">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="068cd-116">Tady je snímek obrazovky aplikace, kterou vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="068cd-116">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="068cd-117">Aplikace používá návrh jednostránkové aplikace (SPA).</span><span class="sxs-lookup"><span data-stu-id="068cd-117">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="068cd-118">"Jednostránková aplikace" je obecný termín pro webovou aplikaci, která načte jednu stránku HTML a pak dynamicky aktualizuje stránku místo načtení nových stránek.</span><span class="sxs-lookup"><span data-stu-id="068cd-118">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="068cd-119">Po počátečním načtení stránky aplikace mluví se serverem prostřednictvím požadavků AJAX.</span><span class="sxs-lookup"><span data-stu-id="068cd-119">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="068cd-120">AJAX požaduje návratová data JSON, která aplikace používá k aktualizaci uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="068cd-120">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="068cd-121">AJAX není novinkou, ale dnes existují rozhraní JavaScript, která usnadňují vytváření a údržbu rozsáhlých sofistikovaných aplikací SPA.</span><span class="sxs-lookup"><span data-stu-id="068cd-121">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="068cd-122">V tomto kurzu se používá [vyseknutí. js](http://knockoutjs.com/), ale můžete použít libovolné klientské rozhraní JavaScript.</span><span class="sxs-lookup"><span data-stu-id="068cd-122">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="068cd-123">Tady jsou hlavní stavební kameny této aplikace:</span><span class="sxs-lookup"><span data-stu-id="068cd-123">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="068cd-124">ASP.NET MVC vytvoří stránku HTML.</span><span class="sxs-lookup"><span data-stu-id="068cd-124">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="068cd-125">Webové rozhraní API ASP.NET zpracovává požadavky AJAX a vrací data JSON.</span><span class="sxs-lookup"><span data-stu-id="068cd-125">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="068cd-126">Vyseknutí dat. js – sváže prvky HTML s daty JSON.</span><span class="sxs-lookup"><span data-stu-id="068cd-126">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="068cd-127">Entity Framework mluví s databází.</span><span class="sxs-lookup"><span data-stu-id="068cd-127">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="068cd-128">Podívejte se na tuto aplikaci spuštěnou v Azure</span><span class="sxs-lookup"><span data-stu-id="068cd-128">See this app running on Azure</span></span>

<span data-ttu-id="068cd-129">Chcete zobrazit dokončený web běžící jako živá webová aplikace?</span><span class="sxs-lookup"><span data-stu-id="068cd-129">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="068cd-130">Úplnou verzi aplikace můžete nasadit do svého účtu Azure tak, že vyberete následující tlačítko.</span><span class="sxs-lookup"><span data-stu-id="068cd-130">You can deploy a complete version of the app to your Azure account by selecting the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="068cd-131">K nasazení tohoto řešení do Azure potřebujete účet Azure.</span><span class="sxs-lookup"><span data-stu-id="068cd-131">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="068cd-132">Pokud ještě nemáte účet, máte následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="068cd-132">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="068cd-133">[Otevřete si bezplatný účet Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – získáte kredity, které můžete použít k vyzkoušení placených služeb Azure a dokonce i po jejich použití, můžete účet ponechat a používat bezplatné služby Azure.</span><span class="sxs-lookup"><span data-stu-id="068cd-133">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="068cd-134">[Aktivujte výhody pro předplatitele MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) – vaše předplatné MSDN vám každý měsíc dává kredity, které můžete použít pro placené služby Azure.</span><span class="sxs-lookup"><span data-stu-id="068cd-134">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="068cd-135">Vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="068cd-135">Create the project</span></span>

<span data-ttu-id="068cd-136">Otevřete sadu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="068cd-136">Open Visual Studio.</span></span> <span data-ttu-id="068cd-137">V nabídce **soubor** vyberte **Nový**a pak vyberte **projekt**.</span><span class="sxs-lookup"><span data-stu-id="068cd-137">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="068cd-138">(Nebo na úvodní stránce vyberte **Nový projekt** .)</span><span class="sxs-lookup"><span data-stu-id="068cd-138">(Or select **New Project** on the Start page.)</span></span>

<span data-ttu-id="068cd-139">V dialogovém okně **Nový projekt** vyberte v levém podokně možnost **Web** a v prostředním podokně **ASP.NET webová aplikace (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="068cd-139">In the **New Project** dialog, select **Web** in the left pane and **ASP.NET Web Application (.NET Framework)** in the middle pane.</span></span> <span data-ttu-id="068cd-140">Pojmenujte projekt **BookService** a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="068cd-140">Name the project **BookService** and select **OK**.</span></span>

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

<span data-ttu-id="068cd-141">V dialogovém okně **Nový projekt ASP.NET** vyberte šablonu **webové rozhraní API** .</span><span class="sxs-lookup"><span data-stu-id="068cd-141">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

<span data-ttu-id="068cd-142">Vyberte **OK** a vytvořte projekt.</span><span class="sxs-lookup"><span data-stu-id="068cd-142">Select **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="068cd-143">Konfigurace nastavení Azure (volitelné)</span><span class="sxs-lookup"><span data-stu-id="068cd-143">Configure Azure settings (optional)</span></span>

<span data-ttu-id="068cd-144">Po vytvoření projektu můžete zvolit, že se má Azure App Service Web Apps kdykoli nasadit.</span><span class="sxs-lookup"><span data-stu-id="068cd-144">After you create the project, you can choose to deploy to Azure App Service Web Apps at any time.</span></span> 

1. <span data-ttu-id="068cd-145">V Průzkumník řešení klikněte pravým tlačítkem na projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="068cd-145">In Solution Explorer, right-click on your project and select **Publish**.</span></span>

2. <span data-ttu-id="068cd-146">V okně, které se zobrazí, vyberte **Spustit**.</span><span class="sxs-lookup"><span data-stu-id="068cd-146">In the window that appears, select **Start**.</span></span> <span data-ttu-id="068cd-147">Zobrazí se dialogové okno **vybrat cíl publikování** .</span><span class="sxs-lookup"><span data-stu-id="068cd-147">The **Pick a publish target** dialog box appears.</span></span>

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. <span data-ttu-id="068cd-148">Vyberte **vytvořit profil**.</span><span class="sxs-lookup"><span data-stu-id="068cd-148">Select **Create Profile**.</span></span> <span data-ttu-id="068cd-149">Zobrazí se dialogové okno **vytvořit App Service** .</span><span class="sxs-lookup"><span data-stu-id="068cd-149">The **Create App Service** dialog box appears.</span></span>

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   <span data-ttu-id="068cd-150">Přijměte výchozí hodnoty nebo zadejte jiné hodnoty pro název aplikace, skupinu prostředků, plán hostování, předplatné Azure a geografickou oblast.</span><span class="sxs-lookup"><span data-stu-id="068cd-150">Accept the defaults, or enter different values for the application name, resource group, hosting plan, Azure subscription, and geographical region.</span></span> 

4. <span data-ttu-id="068cd-151">Vyberte **vytvořit databázi SQL**.</span><span class="sxs-lookup"><span data-stu-id="068cd-151">Select **Create a SQL database**.</span></span> <span data-ttu-id="068cd-152">Zobrazí se dialogové okno **konfigurace SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="068cd-152">The **Configure SQL Server** dialog box appears.</span></span> 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   <span data-ttu-id="068cd-153">Přijměte výchozí hodnoty nebo zadejte jiné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="068cd-153">Accept the defaults or enter different values.</span></span> <span data-ttu-id="068cd-154">Zadejte **uživatelské jméno správce** a **heslo správce** pro novou databázi.</span><span class="sxs-lookup"><span data-stu-id="068cd-154">Enter an **Administrator Username** and **Administrator Password** for your new database.</span></span> <span data-ttu-id="068cd-155">Až budete hotovi, vyberte **OK** .</span><span class="sxs-lookup"><span data-stu-id="068cd-155">Select **OK** when you're done.</span></span> <span data-ttu-id="068cd-156">Znovu se zobrazí stránka **vytvořit App Service** .</span><span class="sxs-lookup"><span data-stu-id="068cd-156">The **Create App Service** page reappears.</span></span>

5. <span data-ttu-id="068cd-157">Vyberte **vytvořit** a vytvořte svůj profil.</span><span class="sxs-lookup"><span data-stu-id="068cd-157">Select **Create** to create your profile.</span></span> <span data-ttu-id="068cd-158">V pravém dolním rohu se zobrazí zpráva s informacemi o tom, že nasazení probíhá.</span><span class="sxs-lookup"><span data-stu-id="068cd-158">A message appears in the lower-right corner indicating that deployment is in progress.</span></span> <span data-ttu-id="068cd-159">Po krátké době se okno **publikování** znovu zobrazí.</span><span class="sxs-lookup"><span data-stu-id="068cd-159">After a short while, the **Publish** window reappears.</span></span>

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    <span data-ttu-id="068cd-160">Profil, který jste vytvořili pro nasazení aplikace, je nyní k dispozici.</span><span class="sxs-lookup"><span data-stu-id="068cd-160">The profile you created to deploy the app is now available.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="068cd-161">Next</span><span class="sxs-lookup"><span data-stu-id="068cd-161">Next</span></span>](part-2.md)
