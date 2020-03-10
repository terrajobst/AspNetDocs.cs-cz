---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Použití signalizace s Web Apps v Azure App Service | Microsoft Docs
author: bradygaster
description: Tento dokument popisuje, jak nakonfigurovat aplikaci signalizace, která běží na Microsoft Azure. Verze softwaru používané v tomto kurzu Visual Studio 2013 nebo VIS...
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558700"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a><span data-ttu-id="ae2e1-104">Použití aplikace SignalR s webovými aplikacemi ve službě Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ae2e1-104">Using SignalR with Web Apps in Azure App Service</span></span>

<span data-ttu-id="ae2e1-105">Po [Fletcheru](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ae2e1-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ae2e1-106">Tento dokument popisuje, jak nakonfigurovat aplikaci signalizace, která běží na Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-106">This document describes how to configure a SignalR application that runs on Microsoft Azure.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ae2e1-107">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="ae2e1-107">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="ae2e1-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) nebo Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="ae2e1-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) or Visual Studio 2012</span></span>
> - <span data-ttu-id="ae2e1-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ae2e1-109">.NET 4.5</span></span>
> - <span data-ttu-id="ae2e1-110">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="ae2e1-110">SignalR version 2</span></span>
> - <span data-ttu-id="ae2e1-111">Sada Azure SDK 2,3 pro Visual Studio 2013 nebo 2012</span><span class="sxs-lookup"><span data-stu-id="ae2e1-111">Azure SDK 2.3 for Visual Studio 2013 or 2012</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="ae2e1-112">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="ae2e1-112">Questions and comments</span></span>
>
> <span data-ttu-id="ae2e1-113">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ae2e1-114">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat na [fórum ASP.NET signálu](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/)nebo [fóra pro Microsoft Azure](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span><span class="sxs-lookup"><span data-stu-id="ae2e1-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), or the [Microsoft Azure forums](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="ae2e1-115">Obsah</span><span class="sxs-lookup"><span data-stu-id="ae2e1-115">Table of Contents</span></span>

- [<span data-ttu-id="ae2e1-116">Úvod</span><span class="sxs-lookup"><span data-stu-id="ae2e1-116">Introduction</span></span>](#introduction)
- [<span data-ttu-id="ae2e1-117">Nasazení webové aplikace Signaler k Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ae2e1-117">Deploying a SignalR Web App to Azure App Service</span></span>](#deploying)
- [<span data-ttu-id="ae2e1-118">Povolování WebSockets na Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ae2e1-118">Enabling WebSockets on Azure App Service</span></span>](#websocket)
- [<span data-ttu-id="ae2e1-119">Použití Azure Redis Cacheho plánu</span><span class="sxs-lookup"><span data-stu-id="ae2e1-119">Using the Azure Redis Cache Backplane</span></span>](#backplane)
- [<span data-ttu-id="ae2e1-120">Další kroky</span><span class="sxs-lookup"><span data-stu-id="ae2e1-120">Next Steps</span></span>](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a><span data-ttu-id="ae2e1-121">Úvod</span><span class="sxs-lookup"><span data-stu-id="ae2e1-121">Introduction</span></span>

<span data-ttu-id="ae2e1-122">Signál ASP.NET lze použít k zajištění nové úrovně interaktivity mezi servery a webovými klienty rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-122">ASP.NET SignalR can be used to bring a new level of interactivity between servers and web or .NET clients.</span></span> <span data-ttu-id="ae2e1-123">Při hostování v Azure můžou aplikace služby Signal využít vysoce dostupné, škálovatelné a výkonné prostředí běžící v cloudu.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-123">When hosted in Azure, SignalR applications can take advantage of the highly available, scalable, and performant environment that running in the cloud provides.</span></span>

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a><span data-ttu-id="ae2e1-124">Nasazení webové aplikace Signaler k Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ae2e1-124">Deploying a SignalR Web App to Azure App Service</span></span>

<span data-ttu-id="ae2e1-125">Návěstí nepřidává žádné konkrétní komplikace k nasazení aplikace do Azure a nasazování na místní server.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-125">SignalR doesn't add any particular complications to deploying an application to Azure versus deploying to an on-premises server.</span></span> <span data-ttu-id="ae2e1-126">Aplikace, která používá signalizaci, může být hostována v Azure bez jakýchkoli změn v konfiguraci a dalších nastaveních (i když podpora soketů WebSockets najdete v tématu [Povolení WebSockets na Azure App Service](#websocket) níže). V tomto kurzu nasadíte aplikaci vytvořenou v [Začínáme kurzu](../getting-started/tutorial-getting-started-with-signalr.md) do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-126">An application that uses SignalR can be hosted in Azure without any changes in configuration or other settings (though for WebSockets support, see [Enabling WebSockets on Azure App Service](#websocket) below.) For this tutorial, you'll deploy the application created in the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) to Azure.</span></span>

<span data-ttu-id="ae2e1-127">**Požadavky**</span><span class="sxs-lookup"><span data-stu-id="ae2e1-127">**Prerequisites**</span></span>

- <span data-ttu-id="ae2e1-128">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-128">Visual Studio 2013.</span></span> <span data-ttu-id="ae2e1-129">Pokud nemáte sadu Visual Studio, Visual Studio 2013 Express for Web je zahrnutý v instalaci sady Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-129">If you don't have Visual Studio, Visual Studio 2013 Express for Web is included in the install of the Azure SDK.</span></span>
- <span data-ttu-id="ae2e1-130">[Sada Azure sdk 2,3 pro Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) nebo [Azure SDK 2,3 pro Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span><span class="sxs-lookup"><span data-stu-id="ae2e1-130">[Azure SDK 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) or [Azure SDK 2.3 for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span></span>
- <span data-ttu-id="ae2e1-131">K dokončení tohoto kurzu budete potřebovat předplatné Azure.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-131">To complete this tutorial, you will need an Azure subscription.</span></span> <span data-ttu-id="ae2e1-132">Můžete [si aktivovat výhody pro předplatitele MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)nebo si [zaregistrovat zkušební předplatné](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae2e1-132">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), or [sign up for a trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

### <a name="deploying-a-signalr-web-app-to-azure"></a><span data-ttu-id="ae2e1-133">Nasazení webové aplikace Signaler do Azure</span><span class="sxs-lookup"><span data-stu-id="ae2e1-133">Deploying a SignalR web app to Azure</span></span>

1. <span data-ttu-id="ae2e1-134">Dokončete [kurz Začínáme](../getting-started/tutorial-getting-started-with-signalr.md)nebo si stáhněte dokončený projekt z [Galerie kódu](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span><span class="sxs-lookup"><span data-stu-id="ae2e1-134">Complete the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the finished project from [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
2. <span data-ttu-id="ae2e1-135">V aplikaci Visual Studio vyberte **sestavení**, **publikovat signál chat**.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-135">In Visual Studio, select **Build**, **Publish SignalR Chat**.</span></span>
3. <span data-ttu-id="ae2e1-136">V dialogovém okně Publikovat web vyberte web Windows Azure weby.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-136">In the "Publish Web" dialog, select "Windows Azure Web Sites".</span></span>

    ![Vybrat weby Azure](using-signalr-with-azure-web-sites/_static/image1.png)
4. <span data-ttu-id="ae2e1-138">Pokud nejste přihlášení k vašemu účet Microsoft, klikněte na **Přihlásit se...** v dialogovém okně vybrat existující web a přihlaste se.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-138">If you aren't signed in to your Microsoft account, click **Sign In...** in the "Select Existing Web Site" dialog, and sign in.</span></span>

    ![Vybrat existující web](using-signalr-with-azure-web-sites/_static/image2.png)    ![Přihlášení k Azure](using-signalr-with-azure-web-sites/_static/image3.png)
5. <span data-ttu-id="ae2e1-141">V dialogovém okně vybrat existující web klikněte na **Nový**.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-141">In the "Select Existing Web Site" dialog, click **New**.</span></span>

    ![Nový web](using-signalr-with-azure-web-sites/_static/image4.png)
6. <span data-ttu-id="ae2e1-143">V dialogovém okně vytvořit web v systému Windows Azure zadejte jedinečný název aplikace.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-143">In the "Create site on Windows Azure" dialog, enter a unique app name.</span></span> <span data-ttu-id="ae2e1-144">V rozevíracím seznamu oblast vyberte oblast, která je nejblíže.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-144">Select the region closest to you in the Region dropdown.</span></span> <span data-ttu-id="ae2e1-145">Klikněte na možnost **Vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-145">Click **Create**.</span></span>

    ![Vytvoření webu v Azure](using-signalr-with-azure-web-sites/_static/image5.png)
7. <span data-ttu-id="ae2e1-147">V dialogovém okně Publikovat web klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-147">In the "Publish Web" dialog, click **Publish**.</span></span>

    ![Publikování webu](using-signalr-with-azure-web-sites/_static/image6.png)
8. <span data-ttu-id="ae2e1-149">Jakmile se aplikace dokončí, otevře se v prohlížeči aplikace chatu signálu, která je hostovaná v Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-149">When the app has completed publishing, the SignalR Chat application hosted in Azure App Service Web Apps will open in a browser.</span></span>

    ![Otevření webu v prohlížeči](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a><span data-ttu-id="ae2e1-151">Povolování WebSockets na Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="ae2e1-151">Enabling WebSockets on Azure App Service Web Apps</span></span>

<span data-ttu-id="ae2e1-152">V aplikaci signalizace je nutné explicitně povolit objekty WebSockets, aby je bylo možné použít v aplikaci signalizace. v opačném případě budou použity jiné protokoly (podrobnosti viz [přenosové a záložní](../getting-started/introduction-to-signalr.md#transports) verze).</span><span class="sxs-lookup"><span data-stu-id="ae2e1-152">WebSockets needs to be explicitly enabled in your web app to be used in a SignalR application; otherwise, other protocols will be used (See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for details).</span></span>

<span data-ttu-id="ae2e1-153">Aby bylo možné použít objekty WebSocket v Azure App Service Web Apps, povolte ji v konfiguračním oddílu webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-153">In order to use WebSockets on Azure App Service Web Apps, enable it in the configuration section of the web app.</span></span> <span data-ttu-id="ae2e1-154">Uděláte to tak, že otevřete webovou aplikaci ve [službě Azure portál pro správu](https://manage.windowsazure.com/)a pak vyberete konfigurovat.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-154">To do this, open your web app in the [Azure Management Portal](https://manage.windowsazure.com/), and select Configure.</span></span>

![Karta Konfigurace](using-signalr-with-azure-web-sites/_static/image8.png)

<span data-ttu-id="ae2e1-156">V horní části stránky konfigurace ověřte, že se pro vaši webovou aplikaci používá .NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-156">At the top of the configuration page, ensure that .NET 4.5 is used for your web app.</span></span>

![Nastavení rozhraní .NET Framework verze 4,5](using-signalr-with-azure-web-sites/_static/image9.png)

<span data-ttu-id="ae2e1-158">Na stránce konfigurace v nastavení **WebSockets** vyberte **zapnuto**.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-158">On the configuration page, in the **WebSockets** setting, select **On**.</span></span>

![Nastavení WebSockets: zapnuto](using-signalr-with-azure-web-sites/_static/image10.png)

<span data-ttu-id="ae2e1-160">V dolní části stránky konfigurace vyberte **Uložit** a uložte provedené změny.</span><span class="sxs-lookup"><span data-stu-id="ae2e1-160">At the bottom of the Configuration page, select **Save** to save your changes.</span></span>

![Uložit nastavení](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a><span data-ttu-id="ae2e1-162">Použití Azure Redis Cacheho plánu</span><span class="sxs-lookup"><span data-stu-id="ae2e1-162">Using the Azure Redis Cache Backplane</span></span>

<span data-ttu-id="ae2e1-163">Pokud pro svou webovou aplikaci použijete více instancí a uživatelé těchto instancí musí vzájemně komunikovat (takže například zprávy chatu vytvořené v jedné instanci mohou kontaktovat uživatele připojené k jiným instancím), musí být v aplikaci implementováno [Azure Redis Cache pro replánování](../performance/scaleout-with-redis.md) .</span><span class="sxs-lookup"><span data-stu-id="ae2e1-163">If you use multiple instances for your web app, and the users of those instances need to interact with one another (so that, for instance, chat messages created in one instance can reach the users connected to other instances), the [Azure Redis Cache backplane](../performance/scaleout-with-redis.md) must be implemented in your application.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="ae2e1-164">Další kroky</span><span class="sxs-lookup"><span data-stu-id="ae2e1-164">Next Steps</span></span>

<span data-ttu-id="ae2e1-165">Další informace o Web Apps v Azure App Service najdete v tématu [přehled Web Apps](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span><span class="sxs-lookup"><span data-stu-id="ae2e1-165">For more information on Web Apps in Azure App Service, see [Web Apps overview](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span></span>
