---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Publikování aplikace do Azure Azure App Service | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622386"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="6175d-102">Publikování aplikace do Azure Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6175d-102">Publish the App to Azure Azure App Service</span></span>

<span data-ttu-id="6175d-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6175d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6175d-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="6175d-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="6175d-105">V posledním kroku budete aplikaci publikovat do Azure.</span><span class="sxs-lookup"><span data-stu-id="6175d-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="6175d-106">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="6175d-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="6175d-107">Kliknutí na **publikovat** vyvolá dialog **Publikovat web** .</span><span class="sxs-lookup"><span data-stu-id="6175d-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="6175d-108">Pokud jste při prvním vytvoření projektu zaškrtli políčko **hostitel v cloudu** , připojení a nastavení jsou už nakonfigurované.</span><span class="sxs-lookup"><span data-stu-id="6175d-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="6175d-109">V takovém případě stačí kliknout na kartu **Nastavení** a zaškrtnout &quot;spustit migrace Code First&quot;.</span><span class="sxs-lookup"><span data-stu-id="6175d-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="6175d-110">(Pokud jste na začátku nezkontrolovali **hostitele v cloudu** , postupujte podle pokynů v [následující části](#new-website).)</span><span class="sxs-lookup"><span data-stu-id="6175d-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="6175d-111">Pokud chcete aplikaci nasadit, klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="6175d-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="6175d-112">Průběh publikování můžete zobrazit v okně **aktivity publikování na webu** .</span><span class="sxs-lookup"><span data-stu-id="6175d-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="6175d-113">(V nabídce **zobrazení** vyberte **jiné okna**a pak vyberte **aktivita publikování webu**.)</span><span class="sxs-lookup"><span data-stu-id="6175d-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="6175d-114">Když Visual Studio dokončí nasazení aplikace, výchozí prohlížeč se automaticky otevře na adrese URL nasazeného webu a aplikace, kterou jste vytvořili, je teď spuštěná v cloudu.</span><span class="sxs-lookup"><span data-stu-id="6175d-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="6175d-115">Adresa URL v adresním řádku prohlížeče ukazuje, že lokalita je načítána z Internetu.</span><span class="sxs-lookup"><span data-stu-id="6175d-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="6175d-116">Nasazení na nový web</span><span class="sxs-lookup"><span data-stu-id="6175d-116">Deploying to a New Website</span></span>

<span data-ttu-id="6175d-117">Pokud jste při prvním vytvoření projektu nezkontrolovali možnost **hostitel v cloudu** , můžete teď nakonfigurovat novou webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6175d-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="6175d-118">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="6175d-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="6175d-119">Vyberte kartu **profil** a klikněte na **Microsoft Azure websites**.</span><span class="sxs-lookup"><span data-stu-id="6175d-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="6175d-120">Pokud v tuto chvíli nejste přihlášení k Azure, budete vyzváni k přihlášení.</span><span class="sxs-lookup"><span data-stu-id="6175d-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="6175d-121">V dialogovém okně **existující weby** klikněte na **Nový**.</span><span class="sxs-lookup"><span data-stu-id="6175d-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="6175d-122">Zadejte název webu.</span><span class="sxs-lookup"><span data-stu-id="6175d-122">Enter a site name.</span></span> <span data-ttu-id="6175d-123">Vyberte své předplatné Azure a oblast.</span><span class="sxs-lookup"><span data-stu-id="6175d-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="6175d-124">V části **databázový server**vyberte **vytvořit nový server**nebo vyberte existující server.</span><span class="sxs-lookup"><span data-stu-id="6175d-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="6175d-125">Klikněte na možnost **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="6175d-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="6175d-126">Klikněte na kartu **Nastavení** a zaškrtněte &quot;spustit migrace Code First&quot;.</span><span class="sxs-lookup"><span data-stu-id="6175d-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="6175d-127">Pak klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="6175d-127">Then click **Publish**.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6175d-128">Předchozí</span><span class="sxs-lookup"><span data-stu-id="6175d-128">Previous</span></span>](part-9.md)
