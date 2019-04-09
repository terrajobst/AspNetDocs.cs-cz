---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Úvod do kurzu NerdDinner | Dokumentace Microsoftu
author: shanselman
description: Nejlepší způsob, jak další nové rozhraní je s ním něco sestavení. Tento kurz vás provede postupem vytvoření malé, ale dokončení aplikace pomocí konfigurace ASP.NE...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: ebd49295ea165ba4ef1a25398cff7dddcfa54f11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392193"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="f1d2a-104">Úvod do kurzu NerdDinner</span><span class="sxs-lookup"><span data-stu-id="f1d2a-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="f1d2a-105">podle [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="f1d2a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="f1d2a-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="f1d2a-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f1d2a-107">Nejlepší způsob, jak další nové rozhraní je s ním něco sestavení.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="f1d2a-108">Tento kurz vás provede postupy vytvoření malé, ale dokončení aplikace pomocí ASP.NET MVC 1 a představuje některé základními koncepcemi jeho fungování.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="f1d2a-109">Pokud používáte ASP.NET MVC 3, doporučujeme je provést [získávání začít s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) kurzy.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-tutorial"></a><span data-ttu-id="f1d2a-110">Do kurzu NerdDinner</span><span class="sxs-lookup"><span data-stu-id="f1d2a-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="f1d2a-111">Nejlepší způsob, jak další nové rozhraní je s ním něco sestavení.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="f1d2a-112">Tento kurz vás provede postupy vytvoření malé, ale dokončení aplikace pomocí ASP.NET MVC a zavádí některé základními koncepcemi jeho fungování.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="f1d2a-113">Aplikace, kterou budeme vytvářet se nazývá "NerdDinner".</span><span class="sxs-lookup"><span data-stu-id="f1d2a-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="f1d2a-114">NerdDinner poskytuje snadný způsob uživatelům najít a uspořádat večeří online:</span><span class="sxs-lookup"><span data-stu-id="f1d2a-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="f1d2a-115">NerdDinner umožňuje vytvářet, upravovat a odstraňovat večeří registrovaných uživatelů.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="f1d2a-116">Vynucuje konzistentní sadu pravidel ověřování a obchodní napříč aplikací:</span><span class="sxs-lookup"><span data-stu-id="f1d2a-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="f1d2a-117">Návštěvníci můžete hledat nadcházející večeří se nachází v jejich mapování na základě AJAX:</span><span class="sxs-lookup"><span data-stu-id="f1d2a-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="f1d2a-118">Kliknutím webu dinner přejdou na stránku podrobností kde lze získat informace Další informace:</span><span class="sxs-lookup"><span data-stu-id="f1d2a-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="f1d2a-119">Pokud se zúčastnili dinner můžou přihlásit nebo zaregistrovat na webu:</span><span class="sxs-lookup"><span data-stu-id="f1d2a-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="f1d2a-120">Můžete pak kliknout na odkaz na reakce na základě jazyka AJAX k Zúčastněte se akce:</span><span class="sxs-lookup"><span data-stu-id="f1d2a-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="f1d2a-121">Implementace NerdDinner</span><span class="sxs-lookup"><span data-stu-id="f1d2a-121">Implementing NerdDinner</span></span>

<span data-ttu-id="f1d2a-122">Budeme zahájíte naší aplikace NerdDinner pomocí souboru -&gt;příkaz Nový projekt v sadě Visual Studio k vytvoření zcela nového projektu ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="f1d2a-123">Pak postupně přidáme funkce a prvky.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="f1d2a-124">Na cestě probereme:</span><span class="sxs-lookup"><span data-stu-id="f1d2a-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="f1d2a-125">Jak vytvořit nový projekt ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f1d2a-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="f1d2a-126">Vytvoření databáze</span><span class="sxs-lookup"><span data-stu-id="f1d2a-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="f1d2a-127">Jak vytvořit model s ověřením obchodních pravidel</span><span class="sxs-lookup"><span data-stu-id="f1d2a-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="f1d2a-128">Použití kontrolerů a zobrazení k implementaci seznamu a podrobností uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="f1d2a-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="f1d2a-129">Postup zajištění akcí CRUD (vytváření, čtení, aktualizace nebo odstranění) podporujících zápis dat do formuláře</span><span class="sxs-lookup"><span data-stu-id="f1d2a-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="f1d2a-130">Použití slovníku ViewData a implementace tříd ViewModel</span><span class="sxs-lookup"><span data-stu-id="f1d2a-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="f1d2a-131">Jak znovu pomocí uživatelského rozhraní pomocí stránek předloh a částečných zobrazení</span><span class="sxs-lookup"><span data-stu-id="f1d2a-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="f1d2a-132">Implementace efektivního stránkování dat</span><span class="sxs-lookup"><span data-stu-id="f1d2a-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="f1d2a-133">Zabezpečení aplikací ověřováním a autorizací</span><span class="sxs-lookup"><span data-stu-id="f1d2a-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="f1d2a-134">Použití jazyka AJAX k dynamickým aktualizacím</span><span class="sxs-lookup"><span data-stu-id="f1d2a-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="f1d2a-135">Použití jazyka AJAX k implementaci scénářů mapování</span><span class="sxs-lookup"><span data-stu-id="f1d2a-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="f1d2a-136">Jak povolit automatické testování částí</span><span class="sxs-lookup"><span data-stu-id="f1d2a-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="f1d2a-137">Můžete vytvořit svoji vlastní kopii NerdDinner úplně od začátku po dokončení každého kroku jsme názorný postup v této kapitole.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="f1d2a-138">Alternativně můžete stáhnout úplnou verzi zdrojového kódu: [NerdDinner na Githubu](https://github.com/AspNetMVPSamples/NerdDinner).</span><span class="sxs-lookup"><span data-stu-id="f1d2a-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="f1d2a-139">Můžete také v případě potřeby také [stáhnout zdarma PDF verzi tohoto kurzu](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) Pokud si chcete přečíst kurz v režimu offline.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="f1d2a-140">Visual Studio 2008 nebo na bezplatné Visual Web Developer 2008 Express můžete použít k sestavení aplikace.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="f1d2a-141">Pro databázi můžete použít SQL Server nebo bezplatný systém SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="f1d2a-142">ASP.NET MVC, Visual Web Developer 2008 Express a SQL Server Express (vše zdarma) pomocí verzí V2 můžete nainstalovat [instalačního programu webové platformy](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="f1d2a-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="f1d2a-143">Nyní můžeme začít...</span><span class="sxs-lookup"><span data-stu-id="f1d2a-143">Now let's get started....</span></span>

<span data-ttu-id="f1d2a-144">Teď, když jsme si popsali, co je NerdDinner, Pojďme vyhrňte rukávy naše a napsání kódu.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="f1d2a-145">Začneme budete pomocí souboru -&gt;nový projekt v sadě Visual Studio k vytvoření aplikace NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="f1d2a-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f1d2a-146">Next</span><span class="sxs-lookup"><span data-stu-id="f1d2a-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
