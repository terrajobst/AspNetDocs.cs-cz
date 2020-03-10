---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Úvod do kurzu NerdDinner | Microsoft Docs
author: shanselman
description: Nejlepším způsobem, jak se naučit nové rozhraní, je vytvořit s ním něco. Tento kurz vás provede vytvořením malé, ale dokončené aplikace s využitím ASP.NE...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580575"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="8191b-104">Úvod do kurzu NerdDinner</span><span class="sxs-lookup"><span data-stu-id="8191b-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="8191b-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="8191b-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="8191b-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="8191b-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="8191b-107">Nejlepším způsobem, jak se naučit nové rozhraní, je vytvořit s ním něco.</span><span class="sxs-lookup"><span data-stu-id="8191b-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="8191b-108">V tomto kurzu se dozvíte, jak vytvořit malou, ale ucelenou aplikaci s využitím ASP.NET MVC 1 a přináší některé základní koncepty.</span><span class="sxs-lookup"><span data-stu-id="8191b-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="8191b-109">Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.</span><span class="sxs-lookup"><span data-stu-id="8191b-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-tutorial"></a><span data-ttu-id="8191b-110">Kurz k NerdDinner</span><span class="sxs-lookup"><span data-stu-id="8191b-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="8191b-111">Nejlepším způsobem, jak se naučit nové rozhraní, je vytvořit s ním něco.</span><span class="sxs-lookup"><span data-stu-id="8191b-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="8191b-112">V tomto kurzu se dozvíte, jak vytvořit malou, ale ucelenou aplikaci s využitím ASP.NET MVC a přináší některé základní koncepty.</span><span class="sxs-lookup"><span data-stu-id="8191b-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="8191b-113">Aplikace, kterou se chystáme sestavit, se nazývá "NerdDinner".</span><span class="sxs-lookup"><span data-stu-id="8191b-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="8191b-114">NerdDinner poskytuje snadný způsob, jak lidem najít a uspořádat večeři online:</span><span class="sxs-lookup"><span data-stu-id="8191b-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="8191b-115">NerdDinner umožňuje registrovaným uživatelům vytvářet, upravovat a odstraňovat večeře.</span><span class="sxs-lookup"><span data-stu-id="8191b-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="8191b-116">Vynutila konzistentní sadu ověřovacích a obchodních pravidel napříč aplikací:</span><span class="sxs-lookup"><span data-stu-id="8191b-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="8191b-117">Návštěvníci můžou k hledání nadcházejících večeře v blízkosti použít mapu založenou na AJAX:</span><span class="sxs-lookup"><span data-stu-id="8191b-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="8191b-118">Kliknutím na večeři přejdete na stránku s podrobnostmi, na které se můžou dozvědět víc.</span><span class="sxs-lookup"><span data-stu-id="8191b-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="8191b-119">Pokud vás zajímá účast na večeři, můžou se na webu přihlásit nebo zaregistrovat:</span><span class="sxs-lookup"><span data-stu-id="8191b-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="8191b-120">Potom můžou kliknout na odkaz na protokol RSVP na základě AJAX a zúčastnit se události:</span><span class="sxs-lookup"><span data-stu-id="8191b-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="8191b-121">Implementace NerdDinner</span><span class="sxs-lookup"><span data-stu-id="8191b-121">Implementing NerdDinner</span></span>

<span data-ttu-id="8191b-122">Spustíme naši aplikaci NerdDinner pomocí příkazu soubor-&gt;nový projekt v sadě Visual Studio k vytvoření značky nového projektu ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="8191b-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="8191b-123">Postupně budeme přidávat funkce a funkce.</span><span class="sxs-lookup"><span data-stu-id="8191b-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="8191b-124">Jak pokryjeme:</span><span class="sxs-lookup"><span data-stu-id="8191b-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="8191b-125">Vytvoření nového projektu ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="8191b-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="8191b-126">Vytvoření databáze</span><span class="sxs-lookup"><span data-stu-id="8191b-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="8191b-127">Jak vytvořit model s ověřováním obchodních pravidel</span><span class="sxs-lookup"><span data-stu-id="8191b-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="8191b-128">Použití řadičů a zobrazení k implementaci uživatelského rozhraní pro výpisy a podrobnosti</span><span class="sxs-lookup"><span data-stu-id="8191b-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="8191b-129">Jak poskytnout položku CRUD (vytvořit, číst, aktualizovat, odstranit) podporu zadávání datových formulářů</span><span class="sxs-lookup"><span data-stu-id="8191b-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="8191b-130">Jak používat ViewData a implementovat třídy ViewModel</span><span class="sxs-lookup"><span data-stu-id="8191b-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="8191b-131">Postup opětovného použití uživatelského rozhraní pomocí stránek předlohy a částečně</span><span class="sxs-lookup"><span data-stu-id="8191b-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="8191b-132">Implementace efektivního stránkování dat</span><span class="sxs-lookup"><span data-stu-id="8191b-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="8191b-133">Zabezpečení aplikací pomocí ověřování a autorizace</span><span class="sxs-lookup"><span data-stu-id="8191b-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="8191b-134">Použití jazyka AJAX k doručování dynamických aktualizací</span><span class="sxs-lookup"><span data-stu-id="8191b-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="8191b-135">Použití jazyka AJAX k implementaci scénářů mapování</span><span class="sxs-lookup"><span data-stu-id="8191b-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="8191b-136">Jak povolit automatizované testování částí</span><span class="sxs-lookup"><span data-stu-id="8191b-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="8191b-137">Můžete vytvořit vlastní kopii NerdDinner od začátku, a to tak, že v této kapitole provedete všechny kroky.</span><span class="sxs-lookup"><span data-stu-id="8191b-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="8191b-138">Případně můžete stáhnout dokončenou verzi zdrojového kódu zde: [NerdDinner na GitHubu](https://github.com/AspNetMVPSamples/NerdDinner).</span><span class="sxs-lookup"><span data-stu-id="8191b-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="8191b-139">Pokud chcete tento kurz Přečtěte offline, můžete také volitelně [Stáhnout bezplatnou verzi tohoto kurzu ve formátu PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) .</span><span class="sxs-lookup"><span data-stu-id="8191b-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="8191b-140">K sestavení aplikace můžete použít buď Visual Studio 2008, nebo bezplatný Visual Web Developer 2008 Express.</span><span class="sxs-lookup"><span data-stu-id="8191b-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="8191b-141">Pro databázi můžete použít buď SQL Server, nebo bezplatný SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="8191b-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="8191b-142">ASP.NET MVC, Visual Web Developer 2008 Express a SQL Server Express (zdarma) můžete nainstalovat pomocí v2 [Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="8191b-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="8191b-143">Pojďme začít....</span><span class="sxs-lookup"><span data-stu-id="8191b-143">Now let's get started....</span></span>

<span data-ttu-id="8191b-144">Teď, když jsme pokryli, co je to NerdDinner, připravujeme naše rukávy a napíšeme kód.</span><span class="sxs-lookup"><span data-stu-id="8191b-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="8191b-145">Zahájíme použití souborového&gt;nového projektu v sadě Visual Studio k vytvoření aplikace v NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="8191b-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8191b-146">Next</span><span class="sxs-lookup"><span data-stu-id="8191b-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
