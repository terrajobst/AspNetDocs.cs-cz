---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: Instalace pomocné rutiny na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek popisuje, jak nainstalovat pomocníka na webu ASP.NET Web Pages (Razor). Pomocná součást je opakovaně použitelná komponenta, která obsahuje kód a kód pro...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638584"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="00d07-104">Instalace pomocné rutiny na webu ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="00d07-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="00d07-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="00d07-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="00d07-106">Tento článek popisuje, jak nainstalovat pomocníka na webu ASP.NET Web Pages (Razor).</span><span class="sxs-lookup"><span data-stu-id="00d07-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="00d07-107">*Pomocná* komponenta je opakovaně použitelná součást, která obsahuje kód a kód k provedení úlohy, která může být zdlouhavá nebo složitá.</span><span class="sxs-lookup"><span data-stu-id="00d07-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="00d07-108">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="00d07-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="00d07-109">Postup instalace Pomocníka na webu vytvořeném pomocí WebMatrixu 3.</span><span class="sxs-lookup"><span data-stu-id="00d07-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="00d07-110">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="00d07-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="00d07-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="00d07-111">WebMatrix 3</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="00d07-112">Přehled pomocníků</span><span class="sxs-lookup"><span data-stu-id="00d07-112">Overview of Helpers</span></span>

<span data-ttu-id="00d07-113">Některé úlohy, které uživatelé často chtějí dělat na webových stránkách, vyžadují velké množství kódu nebo vyžadují další znalosti.</span><span class="sxs-lookup"><span data-stu-id="00d07-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="00d07-114">Mezi příklady patří zobrazení grafu pro data; na stránce se zobrazí tlačítko sledování na Twitteru. odesílání e-mailů z webu oříznutí a změna velikosti imagí; používání služby PayPal pro váš web.</span><span class="sxs-lookup"><span data-stu-id="00d07-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="00d07-115">Aby bylo možné tyto druhy věcí snadno provést, ASP.NET webové stránky vám umožní používat *pomocníka*.</span><span class="sxs-lookup"><span data-stu-id="00d07-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="00d07-116">Pomocníky jsou komponenty, které nainstalujete pro lokalitu a umožňují provádět typické úlohy pomocí pouze řádku nebo dvou kódů Razor.</span><span class="sxs-lookup"><span data-stu-id="00d07-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="00d07-117">ASP.NET webové stránky mají několik vestavěných pomocníků.</span><span class="sxs-lookup"><span data-stu-id="00d07-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="00d07-118">Mnoho pomocníků je však dostupných v balíčcích (Doplňky), které jsou k dispozici pomocí Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="00d07-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="00d07-119">NuGet umožňuje vybrat balíček, který se má nainstalovat, a pak se postará o všechny podrobnosti o instalaci.</span><span class="sxs-lookup"><span data-stu-id="00d07-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="00d07-120">Instalace pomocné rutiny v WebMatrixu 3</span><span class="sxs-lookup"><span data-stu-id="00d07-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="00d07-121">V části WebMatrix 3 klikněte na tlačítko **NuGet** .</span><span class="sxs-lookup"><span data-stu-id="00d07-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![Dialogové okno galerie NuGet v WebMatrixu](installing-helpers/_static/image1.png)
2. <span data-ttu-id="00d07-123">Spustí se správce balíčků NuGet a zobrazí dostupné balíčky.</span><span class="sxs-lookup"><span data-stu-id="00d07-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="00d07-124">Do vyhledávacího pole zadejte klíčové slovo pro pomoc, kterou chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="00d07-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![Dialogové okno galerie NuGet v WebMatrixu](installing-helpers/_static/image2.png)
3. <span data-ttu-id="00d07-126">Vyberte balíček a pak klikněte na **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="00d07-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="00d07-127">Po zobrazení výzvy klikněte na tlačítko **Ano** , pokud chcete balíček nainstalovat a označit, že souhlasíte s podmínkami.</span><span class="sxs-lookup"><span data-stu-id="00d07-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="00d07-128">Pokud jste pomocníka nainstalovali poprvé, vytvoří NuGet ve vašem webu složky pro kód, který tvoří pomoc.</span><span class="sxs-lookup"><span data-stu-id="00d07-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="00d07-129">Chcete-li odinstalovat pomocníka, klikněte na tlačítko **Galerie** , klikněte na kartu **nainstalované** a vyberte balíček, který chcete odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="00d07-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="00d07-130">Instalace pomocníka pro Twitter</span><span class="sxs-lookup"><span data-stu-id="00d07-130">Installing the Twitter helper</span></span>

<span data-ttu-id="00d07-131">Nejnovější verze rozhraní Twitter API není kompatibilní s pomocníkem pro Twitter, který nainstalujete přes NuGet.</span><span class="sxs-lookup"><span data-stu-id="00d07-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="00d07-132">Místo toho se podívejte na informace o tom, jak v projektu nastavit pomocníka pro Twitter, v tématu [WebMatrix Pomocník pro Twitter](twitter-helper.md) .</span><span class="sxs-lookup"><span data-stu-id="00d07-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="00d07-133">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="00d07-133">Additional Resources</span></span>

[<span data-ttu-id="00d07-134">Představujeme ASP.NET webové stránky 2 – základy programování</span><span class="sxs-lookup"><span data-stu-id="00d07-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="00d07-135">Pomocník pro Twitter s webmatrixem</span><span class="sxs-lookup"><span data-stu-id="00d07-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)
