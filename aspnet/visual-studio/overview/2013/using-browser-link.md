---
uid: visual-studio/overview/2013/using-browser-link
title: Používá se odkaz na prohlížeč v Visual Studio 2013 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622904"
---
# <a name="using-browser-link-in-visual-studio-2013"></a><span data-ttu-id="83f85-102">Použití odkazu prohlížeče v Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="83f85-102">Using Browser Link in Visual Studio 2013</span></span>

<span data-ttu-id="83f85-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="83f85-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="83f85-104">Odkaz na prohlížeč je nová funkce v Visual Studio 2013, která vytvoří komunikační kanál mezi vývojovým prostředím a jedním nebo více webovými prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="83f85-104">Browser Link is a new feature in Visual Studio 2013 that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="83f85-105">Odkaz na prohlížeč můžete použít k aktualizaci webové aplikace v několika prohlížečích najednou, což je užitečné pro testování v různých prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="83f85-105">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

- [<span data-ttu-id="83f85-106">Aktualizace prohlížeče</span><span class="sxs-lookup"><span data-stu-id="83f85-106">Browser Refresh</span></span>](#browser-refresh)
- [<span data-ttu-id="83f85-107">Zobrazení řídicího panelu pro odkaz na prohlížeč</span><span class="sxs-lookup"><span data-stu-id="83f85-107">Viewing the Browser Link Dashboard</span></span>](#dashboard)
- [<span data-ttu-id="83f85-108">Povolení odkazu na prohlížeč pro statické soubory HTML</span><span class="sxs-lookup"><span data-stu-id="83f85-108">Enabling Browser Link for Static HTML Files</span></span>](#static-html)
- [<span data-ttu-id="83f85-109">Zakazuje se odkaz na prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="83f85-109">Disabling Browser Link</span></span>](#disabling)
- [<span data-ttu-id="83f85-110">Jak to funguje?</span><span class="sxs-lookup"><span data-stu-id="83f85-110">How Does It Work?</span></span>](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a><span data-ttu-id="83f85-111">Aktualizace prohlížeče</span><span class="sxs-lookup"><span data-stu-id="83f85-111">Browser Refresh</span></span>

<span data-ttu-id="83f85-112">Pomocí aktualizace prohlížeče můžete aktualizovat několik prohlížečů, které jsou připojené k aplikaci Visual Studio prostřednictvím odkazu Browser.</span><span class="sxs-lookup"><span data-stu-id="83f85-112">With Browser Refresh, you can refresh multiple browsers that are connected to Visual Studio through Browser Link.</span></span>

<span data-ttu-id="83f85-113">Chcete-li použít aktualizaci prohlížeče, nejprve vytvořte aplikaci ASP.NET pomocí některé z šablon projektu.</span><span class="sxs-lookup"><span data-stu-id="83f85-113">To use Browser Refresh, first create an ASP.NET application, using any of the project templates.</span></span> <span data-ttu-id="83f85-114">Ladění aplikace stisknutím klávesy F5 nebo kliknutím na ikonu se šipkou na panelu nástrojů:</span><span class="sxs-lookup"><span data-stu-id="83f85-114">Debug the application by pressing F5 or clicking the arrow icon in the toolbar:</span></span>

![](using-browser-link/_static/image1.png)

<span data-ttu-id="83f85-115">Pomocí rozevíracího seznamu můžete také vybrat konkrétní prohlížeč pro ladění.</span><span class="sxs-lookup"><span data-stu-id="83f85-115">You can also use the dropdown to select a specific browser for debugging.</span></span>

![](using-browser-link/_static/image2.png)

<span data-ttu-id="83f85-116">Chcete-li ladit více prohlížečů, vyberte možnost **Procházet pomocí**.</span><span class="sxs-lookup"><span data-stu-id="83f85-116">To debug with multiple browsers, select **Browse With**.</span></span> <span data-ttu-id="83f85-117">V dialogovém okně **Procházet se** stisknutím klávesy Ctrl vyberte více než jeden prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="83f85-117">In the **Browse With** dialog, hold down the CTRL key to select more than one browser.</span></span> <span data-ttu-id="83f85-118">Kliknutím na **Procházet** můžete ladit s vybranými prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="83f85-118">Click **Browse** to debug with the selected browsers.</span></span> <span data-ttu-id="83f85-119">Odkaz na prohlížeč funguje také v případě, že spustíte prohlížeč mimo aplikaci Visual Studio a přejdete na adresu URL aplikace.</span><span class="sxs-lookup"><span data-stu-id="83f85-119">Browser Link also works if you launch a browser from outside Visual Studio and navigate to the application URL.</span></span>

![](using-browser-link/_static/image3.png)

<span data-ttu-id="83f85-120">Ovládací prvky Browser Link se nacházejí v rozevíracím seznamu s kulatou ikonou šipky.</span><span class="sxs-lookup"><span data-stu-id="83f85-120">The Browser Link controls are located in the dropdown with the circular arrow icon.</span></span> <span data-ttu-id="83f85-121">Ikona šipky je tlačítko **aktualizovat** .</span><span class="sxs-lookup"><span data-stu-id="83f85-121">The arrow icon is the **Refresh** button.</span></span>

![](using-browser-link/_static/image4.png)

<span data-ttu-id="83f85-122">Pokud chcete zjistit, které prohlížeče jsou připojené, najeďte myší na tlačítko **aktualizovat** při ladění.</span><span class="sxs-lookup"><span data-stu-id="83f85-122">To see which browsers are connected, hover the mouse over the **Refresh** button while debugging.</span></span> <span data-ttu-id="83f85-123">Připojené prohlížeče se zobrazí v okně s popisem.</span><span class="sxs-lookup"><span data-stu-id="83f85-123">The connected browsers are shown in a ToolTip window.</span></span>

![](using-browser-link/_static/image5.png)

<span data-ttu-id="83f85-124">Chcete-li aktualizovat připojené prohlížeče, klikněte na tlačítko **aktualizovat** nebo stiskněte klávesy CTRL + ALT + ENTER.</span><span class="sxs-lookup"><span data-stu-id="83f85-124">To refresh the connected browsers, click the **Refresh** button or press CTRL+ALT+ENTER.</span></span> <span data-ttu-id="83f85-125">Například následující snímek obrazovky ukazuje projekt ASP.NET, který byl vytvořen pomocí šablony projektu MVC 5.</span><span class="sxs-lookup"><span data-stu-id="83f85-125">For example, the following screenshot shows an ASP.NET project, which I created using the MVC 5 project template.</span></span> <span data-ttu-id="83f85-126">V horní části můžete vidět aplikaci spuštěnou ve dvou prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="83f85-126">You can see the application running in two browsers at the top.</span></span> <span data-ttu-id="83f85-127">V dolní části je projekt otevřen v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83f85-127">At the bottom, the project is open in Visual Studio.</span></span>

![](using-browser-link/_static/image6.png)

<span data-ttu-id="83f85-128">V aplikaci Visual Studio jsem změnil (a) &lt;H1&gt; nadpis domovské stránky:</span><span class="sxs-lookup"><span data-stu-id="83f85-128">In Visual Studio, I changed the &lt;h1&gt; heading for the home page:</span></span>

![](using-browser-link/_static/image7.png)

<span data-ttu-id="83f85-129">Po kliknutí na tlačítko **aktualizovat** se změna objevila v obou oknech prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="83f85-129">When I clicked the **Refresh** button, the change appeared in both browser windows:</span></span>

![](using-browser-link/_static/image8.png)

<span data-ttu-id="83f85-130">**Poznámky**</span><span class="sxs-lookup"><span data-stu-id="83f85-130">**Notes**</span></span>

- <span data-ttu-id="83f85-131">Chcete-li povolit odkaz na prohlížeč, nastavte `debug=true` v prvku [&lt;kompilace&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) v souboru Web. config projektu.</span><span class="sxs-lookup"><span data-stu-id="83f85-131">To enable Browser Link, set `debug=true` in the [&lt;compilation&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) element in the project's Web.config file.</span></span>
- <span data-ttu-id="83f85-132">Aplikace musí běžet na místním hostiteli.</span><span class="sxs-lookup"><span data-stu-id="83f85-132">The application must be running on localhost.</span></span>
- <span data-ttu-id="83f85-133">Aplikace musí být cílena na rozhraní .NET 4,0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="83f85-133">The application must target .NET 4.0 or later.</span></span>

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a><span data-ttu-id="83f85-134">Zobrazení řídicího panelu pro odkaz na prohlížeč</span><span class="sxs-lookup"><span data-stu-id="83f85-134">Viewing the Browser Link Dashboard</span></span>

<span data-ttu-id="83f85-135">Řídicí panel propojení prohlížeče zobrazuje informace o připojeních odkazů prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="83f85-135">The Browser Link dashboard shows information about the Browser Link connections.</span></span> <span data-ttu-id="83f85-136">Chcete-li zobrazit řídicí panel, vyberte rozevírací nabídku odkaz prohlížeče (malou šipku vedle tlačítka **aktualizovat** ).</span><span class="sxs-lookup"><span data-stu-id="83f85-136">To view the dashboard, select the Browser Link dropdown menu (the small arrow next to the **Refresh** button).</span></span> <span data-ttu-id="83f85-137">Pak klikněte na **řídicí panel odkaz na prohlížeč**.</span><span class="sxs-lookup"><span data-stu-id="83f85-137">Then click **Browser Link Dashboard**.</span></span>

![](using-browser-link/_static/image9.png)

<span data-ttu-id="83f85-138">Řídicí panel zobrazuje připojené prohlížeče a adresu URL, na které má každý prohlížeč přejít.</span><span class="sxs-lookup"><span data-stu-id="83f85-138">The dashboard lists the connected Browsers and the URL to which each browser has navigated.</span></span>

![](using-browser-link/_static/image10.png)

<span data-ttu-id="83f85-139">V části **požadavky** se zobrazují všechny kroky, které jsou nutné k povolení odkazu na prohlížeč pro daný projekt.</span><span class="sxs-lookup"><span data-stu-id="83f85-139">The **Prerequisites** section shows any steps needed to enable Browser Link for that project.</span></span> <span data-ttu-id="83f85-140">Například následující snímek obrazovky ukazuje projekt, ve kterém je "ladění" v souboru Web. config nastaveno na hodnotu false.</span><span class="sxs-lookup"><span data-stu-id="83f85-140">For example, the following screenshot shows a project where "debug" is set to false in the Web.config file.</span></span>

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a><span data-ttu-id="83f85-141">Povolení odkazu na prohlížeč pro statické soubory HTML</span><span class="sxs-lookup"><span data-stu-id="83f85-141">Enabling Browser Link for Static HTML Files</span></span>

<span data-ttu-id="83f85-142">Chcete-li povolit odkaz na prohlížeč pro statické soubory HTML, přidejte do souboru Web. config následující text.</span><span class="sxs-lookup"><span data-stu-id="83f85-142">To enable Browser Link for static HTML files, add the following to your Web.config file.</span></span>

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

<span data-ttu-id="83f85-143">Z důvodu výkonu odeberte toto nastavení při publikování projektu.</span><span class="sxs-lookup"><span data-stu-id="83f85-143">For performance reasons, remove this setting when you publish your project.</span></span>

<a id="disabling"></a>
## <a name="disabling-browser-link"></a><span data-ttu-id="83f85-144">Zakazuje se odkaz na prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="83f85-144">Disabling Browser Link</span></span>

<span data-ttu-id="83f85-145">Odkaz na prohlížeč je ve výchozím nastavení povolený.</span><span class="sxs-lookup"><span data-stu-id="83f85-145">Browser Link is enabled by default.</span></span> <span data-ttu-id="83f85-146">Je několik způsobů, jak je zakázat:</span><span class="sxs-lookup"><span data-stu-id="83f85-146">There are several ways to disable it:</span></span>

- <span data-ttu-id="83f85-147">V rozevírací nabídce odkaz prohlížeče zrušte **možnost povolit odkaz na prohlížeč**.</span><span class="sxs-lookup"><span data-stu-id="83f85-147">In the Browser Link dropdown menu, uncheck **Enable Browser Link**.</span></span> 

    ![](using-browser-link/_static/image12.png)
- <span data-ttu-id="83f85-148">V souboru Web. config přidejte klíč s názvem "vs: EnableBrowserLink" s hodnotou "false" v oddílu appSettings.</span><span class="sxs-lookup"><span data-stu-id="83f85-148">In the Web.config file, add a key named "vs:EnableBrowserLink" with the value "false" in the appSettings section.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- <span data-ttu-id="83f85-149">V souboru Web. config nastavte Debug na false.</span><span class="sxs-lookup"><span data-stu-id="83f85-149">In the Web.config file, set debug to false.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a><span data-ttu-id="83f85-150">Jak to funguje?</span><span class="sxs-lookup"><span data-stu-id="83f85-150">How Does It Work?</span></span>

<span data-ttu-id="83f85-151">Odkaz na prohlížeč používá [signál](../../../signalr/index.md) k vytvoření komunikačního kanálu mezi Visual Studio a prohlížečem.</span><span class="sxs-lookup"><span data-stu-id="83f85-151">Browser Link uses [SignalR](../../../signalr/index.md) to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="83f85-152">Je-li povolen odkaz na prohlížeč, aplikace Visual Studio funguje jako server signálu, ke kterému se může připojit více klientů (prohlížečů).</span><span class="sxs-lookup"><span data-stu-id="83f85-152">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="83f85-153">Odkaz na prohlížeč také zaregistruje modul HTTP pomocí ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="83f85-153">Browser Link also registers an HTTP module with ASP.NET.</span></span> <span data-ttu-id="83f85-154">Tento modul vloží speciální skript &lt;&gt; odkazuje na každý požadavek stránky ze serveru.</span><span class="sxs-lookup"><span data-stu-id="83f85-154">This module injects special &lt;script&gt; references into every page request from the server.</span></span> <span data-ttu-id="83f85-155">Odkazy na skript můžete zobrazit tak, že v prohlížeči vyberete "Zobrazit zdroj".</span><span class="sxs-lookup"><span data-stu-id="83f85-155">You can see the script references by selecting "View source" in the browser.</span></span>

![](using-browser-link/_static/image13.png)

<span data-ttu-id="83f85-156">Vaše zdrojové soubory se nemění.</span><span class="sxs-lookup"><span data-stu-id="83f85-156">Your source files are not modified.</span></span> <span data-ttu-id="83f85-157">Modul HTTP vloží odkazy skriptu dynamicky.</span><span class="sxs-lookup"><span data-stu-id="83f85-157">The HTTP module injects the script references dynamically.</span></span>

<span data-ttu-id="83f85-158">Vzhledem k tomu, že kód na straně prohlížeče je celý JavaScript, funguje ve všech prohlížečích, které [Signal podporuje](../../../signalr/overview/getting-started/supported-platforms.md), bez vyžadování jakéhokoli modulu plug-in prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="83f85-158">Because the browser-side code is all JavaScript, it works on all browsers that [SignalR supports](../../../signalr/overview/getting-started/supported-platforms.md), without requiring any browser plug-in.</span></span>
