---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: Začínáme s webovými formuláři ASP.NET 4,7 a sadou Visual Studio 2017 | Microsoft Docs
author: Erikre
description: Tato série podrobných kurzů vás seznámí se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,7 a Microsoft Visual Studio
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615457"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a><span data-ttu-id="ce789-103">Začínáme s webovými formuláři ASP.NET 4,5 a sadou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ce789-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2017</span></span>

<span data-ttu-id="ce789-104">[Stáhnout vzorový projekt Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="ce789-104">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="ce789-105">V této sérii kurzů se dozvíte, jak vytvořit aplikaci webových formulářů v ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ce789-105">This tutorial series shows you how to build an ASP.NET Web Forms application with ASP.NET 4.5 and Microsoft Visual Studio 2017.</span></span> 

## <a name="introduction"></a><span data-ttu-id="ce789-106">Úvod</span><span class="sxs-lookup"><span data-stu-id="ce789-106">Introduction</span></span>

<span data-ttu-id="ce789-107">Tato série kurzů vás provede vytvořením aplikace webových formulářů ASP.NET pomocí sady Visual Studio 2017 a ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="ce789-107">This tutorial series guides you through creating an ASP.NET Web Forms application using Visual Studio 2017 and ASP.NET 4.5.</span></span> <span data-ttu-id="ce789-108">Vytvoříte aplikaci s názvem **Wingtip Toys** – zjednodušená webová stránka prezentace prodej položek online.</span><span class="sxs-lookup"><span data-stu-id="ce789-108">You'll create an application named **Wingtip Toys** - a simplified storefront web site selling items online.</span></span> <span data-ttu-id="ce789-109">Během série se zvýrazní nové funkce ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="ce789-109">During the series, new ASP.NET 4.5 features are highlighted.</span></span>

### <a name="target-audience"></a><span data-ttu-id="ce789-110">Cílová skupina</span><span class="sxs-lookup"><span data-stu-id="ce789-110">Target audience</span></span>

<span data-ttu-id="ce789-111">Pro tuto řadu kurzů jsou noví vývojáři pro ASP.NET webové formuláře cílovou skupinou.</span><span class="sxs-lookup"><span data-stu-id="ce789-111">Developers new to ASP.NET Web Forms are the target audience for this tutorial series.</span></span>

<span data-ttu-id="ce789-112">Měli byste mít několik znalostí v následujících oblastech:</span><span class="sxs-lookup"><span data-stu-id="ce789-112">You should have some knowledge in the following areas:</span></span>

- <span data-ttu-id="ce789-113">Objektově orientované programování (OOP) a jazyky</span><span class="sxs-lookup"><span data-stu-id="ce789-113">Object-oriented programming (OOP) and languages</span></span>
- <span data-ttu-id="ce789-114">Vývoj pro web (HTML, CSS, JavaScript)</span><span class="sxs-lookup"><span data-stu-id="ce789-114">Web development (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="ce789-115">Relační databáze</span><span class="sxs-lookup"><span data-stu-id="ce789-115">Relational databases</span></span>
- <span data-ttu-id="ce789-116">N-vrstvá architektura</span><span class="sxs-lookup"><span data-stu-id="ce789-116">N-tier architecture</span></span>

<span data-ttu-id="ce789-117">Pokud si chcete projít tyto oblasti, vezměte v úvahu následující obsah:</span><span class="sxs-lookup"><span data-stu-id="ce789-117">To review these areas, consider studying the following content:</span></span>

- [<span data-ttu-id="ce789-118">Začínáme pomocí vizuáluC#</span><span class="sxs-lookup"><span data-stu-id="ce789-118">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="ce789-119">[Vývoj pro web](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, php, jQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="ce789-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="ce789-120">Relační databáze</span><span class="sxs-lookup"><span data-stu-id="ce789-120">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="ce789-121">Vícevrstvá architektura</span><span class="sxs-lookup"><span data-stu-id="ce789-121">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="ce789-122">Funkce aplikace</span><span class="sxs-lookup"><span data-stu-id="ce789-122">Application features</span></span>

<span data-ttu-id="ce789-123">Mezi funkce webového formuláře ASP.NET prezentované v tomto seriálu patří:</span><span class="sxs-lookup"><span data-stu-id="ce789-123">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="ce789-124">Projekt webové aplikace (ne web projektu)</span><span class="sxs-lookup"><span data-stu-id="ce789-124">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="ce789-125">Webové formuláře</span><span class="sxs-lookup"><span data-stu-id="ce789-125">Web Forms</span></span>
- <span data-ttu-id="ce789-126">Stránky předlohy, konfigurace</span><span class="sxs-lookup"><span data-stu-id="ce789-126">Master Pages, Configuration</span></span>
- <span data-ttu-id="ce789-127">Spouštěcí rutina</span><span class="sxs-lookup"><span data-stu-id="ce789-127">Bootstrap</span></span>
- <span data-ttu-id="ce789-128">Entity Framework Code First, LocalDB</span><span class="sxs-lookup"><span data-stu-id="ce789-128">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="ce789-129">Žádost o ověření</span><span class="sxs-lookup"><span data-stu-id="ce789-129">Request Validation</span></span>
- <span data-ttu-id="ce789-130">Datové ovládací prvky silného typu</span><span class="sxs-lookup"><span data-stu-id="ce789-130">Strongly-typed Data Controls</span></span>
- <span data-ttu-id="ce789-131">Vazba modelu</span><span class="sxs-lookup"><span data-stu-id="ce789-131">Model Binding</span></span>
- <span data-ttu-id="ce789-132">Datové poznámky</span><span class="sxs-lookup"><span data-stu-id="ce789-132">Data Annotations</span></span>
- <span data-ttu-id="ce789-133">Zprostředkovatelé hodnot</span><span class="sxs-lookup"><span data-stu-id="ce789-133">Value Providers</span></span>
- <span data-ttu-id="ce789-134">SSL a OAuth</span><span class="sxs-lookup"><span data-stu-id="ce789-134">SSL and OAuth</span></span>
- <span data-ttu-id="ce789-135">ASP.NET Identity, konfigurace a autorizace</span><span class="sxs-lookup"><span data-stu-id="ce789-135">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="ce789-136">Nenáročná ověření</span><span class="sxs-lookup"><span data-stu-id="ce789-136">Unobtrusive Validation</span></span>
- <span data-ttu-id="ce789-137">Směrování</span><span class="sxs-lookup"><span data-stu-id="ce789-137">Routing</span></span>
- <span data-ttu-id="ce789-138">Zpracování chyb v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ce789-138">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="ce789-139">Scénáře a úlohy aplikací</span><span class="sxs-lookup"><span data-stu-id="ce789-139">Application scenarios and tasks</span></span>

<span data-ttu-id="ce789-140">Úkoly řady kurzů zahrnují:</span><span class="sxs-lookup"><span data-stu-id="ce789-140">Tutorial series tasks include:</span></span>

- <span data-ttu-id="ce789-141">Vytvoření, kontrola a spuštění nového projektu</span><span class="sxs-lookup"><span data-stu-id="ce789-141">Creating, reviewing, and running a new project</span></span>
- <span data-ttu-id="ce789-142">Vytvoření struktury databáze</span><span class="sxs-lookup"><span data-stu-id="ce789-142">Creating a database structure</span></span>
- <span data-ttu-id="ce789-143">Inicializace a osazení databáze</span><span class="sxs-lookup"><span data-stu-id="ce789-143">Initializing and seeding a database</span></span>
- <span data-ttu-id="ce789-144">Přizpůsobení uživatelského rozhraní pomocí stylů, grafiky a stránky předlohy</span><span class="sxs-lookup"><span data-stu-id="ce789-144">Customizing the UI with styles, graphics, and a master page</span></span>
- <span data-ttu-id="ce789-145">Přidávání stránek a navigace</span><span class="sxs-lookup"><span data-stu-id="ce789-145">Adding pages and navigation</span></span>
- <span data-ttu-id="ce789-146">Zobrazení podrobností nabídky a dat produktu</span><span class="sxs-lookup"><span data-stu-id="ce789-146">Displaying menu details and product data</span></span>
- <span data-ttu-id="ce789-147">Vytvoření nákupního košíku</span><span class="sxs-lookup"><span data-stu-id="ce789-147">Creating a shopping cart</span></span>
- <span data-ttu-id="ce789-148">Přidání podpory SSL a OAuth</span><span class="sxs-lookup"><span data-stu-id="ce789-148">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="ce789-149">Přidání způsobu platby</span><span class="sxs-lookup"><span data-stu-id="ce789-149">Adding a payment method</span></span>
- <span data-ttu-id="ce789-150">Zahrnutí role správce a uživatele do aplikace</span><span class="sxs-lookup"><span data-stu-id="ce789-150">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="ce789-151">Omezení přístupu ke konkrétním stránkám a složce</span><span class="sxs-lookup"><span data-stu-id="ce789-151">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="ce789-152">Nahrání souboru do webové aplikace</span><span class="sxs-lookup"><span data-stu-id="ce789-152">Uploading a file to the web application</span></span>
- <span data-ttu-id="ce789-153">Implementace ověřování vstupu</span><span class="sxs-lookup"><span data-stu-id="ce789-153">Implementing input validation</span></span>
- <span data-ttu-id="ce789-154">Registrace tras pro webovou aplikaci</span><span class="sxs-lookup"><span data-stu-id="ce789-154">Registering routes for the web application</span></span>
- <span data-ttu-id="ce789-155">Implementace zpracování chyb a protokolování chyb</span><span class="sxs-lookup"><span data-stu-id="ce789-155">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="ce789-156">Přehled</span><span class="sxs-lookup"><span data-stu-id="ce789-156">Overview</span></span>

<span data-ttu-id="ce789-157">Tato série kurzů je určená pro někoho, kdo se seznámí s koncepty programování, ale novinkou pro ASP.NET webové formuláře.</span><span class="sxs-lookup"><span data-stu-id="ce789-157">This tutorial series is intended for someone familiar with programming concepts, but new to ASP.NET Web Forms.</span></span> <span data-ttu-id="ce789-158">Pokud jste již obeznámeni s webovými formuláři ASP.NET, může vám tato řada stále pomáhat s novými funkcemi ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="ce789-158">If you're already familiar with ASP.NET Web Forms, this series can still help you learn about new ASP.NET 4.5 features.</span></span> <span data-ttu-id="ce789-159">Pro čtenáře, kteří nejsou obeznámeni s koncepty programování a ASP.NET webovými formuláři, si přečtěte další kurzy webových formulářů, které jsou k dispozici v části [Začínáme](../../../index.md) na webu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ce789-159">For readers unfamiliar with programming concepts and ASP.NET Web Forms, see the additional Web Forms tutorials provided in the [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="ce789-160">ASP.NET 4,5 poskytnutý v této sérii kurzů obsahuje následující funkce:</span><span class="sxs-lookup"><span data-stu-id="ce789-160">The ASP.NET 4.5 provided in this tutorial series includes the following features:</span></span>

- <span data-ttu-id="ce789-161">Jednoduché uživatelské rozhraní pro vytváření projektů, které nabízí [podporu pro řadu ASP.NETch platforem](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (webové formuláře, MVC a webové rozhraní API).</span><span class="sxs-lookup"><span data-stu-id="ce789-161">A simple UI for creating projects that offers [support for many ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="ce789-162">[Zavedení](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), rozložení, vytváření a reakce rozhraní návrhu.</span><span class="sxs-lookup"><span data-stu-id="ce789-162">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout, theming, and responsive design framework.</span></span>
- <span data-ttu-id="ce789-163">[ASP.NET identity](../../../../identity/index.md)nový systém členství v ASP.NET, který funguje stejně ve všech ASP.NET architekturách a pracuje s jiným softwarem pro hostování webů, než je služba IIS.</span><span class="sxs-lookup"><span data-stu-id="ce789-163">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- [<span data-ttu-id="ce789-164">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="ce789-164">Entity Framework 6</span></span>](https://msdn.microsoft.com/data/ef.aspx)

  <span data-ttu-id="ce789-165">Aktualizace Entity Framework, která vám umožní:</span><span class="sxs-lookup"><span data-stu-id="ce789-165">An update to the Entity Framework enabling you to:</span></span>
  - <span data-ttu-id="ce789-166">Načtení a manipulace s daty jako objekty silného typu</span><span class="sxs-lookup"><span data-stu-id="ce789-166">Retrieve and manipulate data as strongly-typed objects</span></span>
  - <span data-ttu-id="ce789-167">Asynchronní přístup k datům</span><span class="sxs-lookup"><span data-stu-id="ce789-167">Access data asynchronously</span></span>
  - <span data-ttu-id="ce789-168">Zpracování přechodných chyb připojení</span><span class="sxs-lookup"><span data-stu-id="ce789-168">Handle transient connection faults</span></span>
  - <span data-ttu-id="ce789-169">Log SQL – příkazy</span><span class="sxs-lookup"><span data-stu-id="ce789-169">Log SQL statements</span></span>

<span data-ttu-id="ce789-170">Úplný seznam funkcí ASP.NET 4,5 najdete v tématu [ASP.NET and Web Tools pro Visual Studio 2013 poznámky k verzi](../../../../visual-studio/overview/2013/release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="ce789-170">For a complete ASP.NET 4.5 feature list, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="ce789-171">Ukázková aplikace Wingtip Toys</span><span class="sxs-lookup"><span data-stu-id="ce789-171">The Wingtip Toys sample application</span></span>

<span data-ttu-id="ce789-172">Následující snímky obrazovky jsou z aplikace webových formulářů ASP.NET, kterou vytvoříte v této sérii kurzů.</span><span class="sxs-lookup"><span data-stu-id="ce789-172">The following screenshots are from the ASP.NET Web Forms application that you create in this tutorial series.</span></span> <span data-ttu-id="ce789-173">Při spuštění aplikace v aplikaci Visual Studio se zobrazí následující Domovská stránka webu.</span><span class="sxs-lookup"><span data-stu-id="ce789-173">When you run the application in Visual Studio, the following web Home page appears.</span></span>

![Wingtip Toys – výchozí stránka](introduction-and-overview/_static/image1.png)

<span data-ttu-id="ce789-175">Můžete se zaregistrovat jako nový uživatel nebo se přihlásit jako stávající uživatel.</span><span class="sxs-lookup"><span data-stu-id="ce789-175">You can register as a new user, or sign in as an existing user.</span></span> <span data-ttu-id="ce789-176">Horní navigace obsahuje odkazy na kategorie produktů a jejich produkty z databáze.</span><span class="sxs-lookup"><span data-stu-id="ce789-176">The top navigation has links to product categories and their products from the database.</span></span>

<span data-ttu-id="ce789-177">Pokud vyberete možnost **produkty**, zobrazí se všechny dostupné produkty.</span><span class="sxs-lookup"><span data-stu-id="ce789-177">If you select **Products**, all available products are displayed.</span></span> 

![Společnost Wingtip Toys – produkty](introduction-and-overview/_static/image2.png)

<span data-ttu-id="ce789-179">Pokud vyberete určitý produkt, zobrazí se podrobnosti o produktu.</span><span class="sxs-lookup"><span data-stu-id="ce789-179">If you select a specific product, product details are displayed.</span></span>

![Společnost Wingtip Toys – podrobnosti o produktu](introduction-and-overview/_static/image3.png)

<span data-ttu-id="ce789-181">Jako uživatel můžete registrovat a přihlašovat se pomocí výchozích funkcí šablon webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="ce789-181">As a user, you can register and sign in with Web Forms template default functionality.</span></span> <span data-ttu-id="ce789-182">Tento kurz taky vysvětluje, jak se přihlašovat pomocí existujícího účtu Gmail.</span><span class="sxs-lookup"><span data-stu-id="ce789-182">This tutorial also explains how to sign in using an existing Gmail account.</span></span> <span data-ttu-id="ce789-183">Kromě toho se můžete přihlásit jako správce a přidat nebo odebrat produkty z databáze.</span><span class="sxs-lookup"><span data-stu-id="ce789-183">Additionally, you can sign in as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys – přihlášení](introduction-and-overview/_static/image4.png)

<span data-ttu-id="ce789-185">Jakmile se přihlásíte jako uživatel, můžete přidat produkty do nákupního košíku a zaregistrovat se pomocí služby PayPal.</span><span class="sxs-lookup"><span data-stu-id="ce789-185">Once you've signed in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="ce789-186">Ukázková aplikace je navržená tak, aby fungovala v izolovaném prostoru pro vývojáře ve službě PayPal.</span><span class="sxs-lookup"><span data-stu-id="ce789-186">The sample application is designed to work in PayPal's developer sandbox.</span></span> <span data-ttu-id="ce789-187">Žádná skutečná peněžní transakce se neuskuteční.</span><span class="sxs-lookup"><span data-stu-id="ce789-187">No actual money transaction takes place.</span></span>

![Wingtip Toys – nákupní košík](introduction-and-overview/_static/image5.png)

<span data-ttu-id="ce789-189">PayPal potvrdí informace o vašem účtu, objednávce a platbě.</span><span class="sxs-lookup"><span data-stu-id="ce789-189">PayPal confirms your account, order, and payment information.</span></span>

![Wingtip Toys – PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="ce789-191">Po návratu ze služby PayPal můžete zkontrolovat a dokončit vaši objednávku.</span><span class="sxs-lookup"><span data-stu-id="ce789-191">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys – revize objednávky](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="ce789-193">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ce789-193">Prerequisites</span></span>

<span data-ttu-id="ce789-194">Než začnete, ujistěte se, že je v počítači nainstalovaný následující software:</span><span class="sxs-lookup"><span data-stu-id="ce789-194">Before you start, make sure the following software is installed on your computer:</span></span>

- <span data-ttu-id="ce789-195">[Microsoft Visual Studio 2017 nebo Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ce789-195">[Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span></span>

<span data-ttu-id="ce789-196">.NET Framework se nainstaluje automaticky.</span><span class="sxs-lookup"><span data-stu-id="ce789-196">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="ce789-197">Tato série kurzů používá Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="ce789-197">This tutorial series uses Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="ce789-198">K dokončení této série kurzů můžete použít buď to, nebo Microsoft Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ce789-198">You can use either that or Microsoft Visual Studio 2017 to complete this tutorial series.</span></span>

<span data-ttu-id="ce789-199">Všimněte si následujících informací o aplikaci Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ce789-199">Note the following about Visual Studio:</span></span>

* <span data-ttu-id="ce789-200">Microsoft Visual Studio 2017 a Microsoft Visual Studio Community 2017 se v této sérii kurzů označují jako *Visual Studio* .</span><span class="sxs-lookup"><span data-stu-id="ce789-200">Microsoft Visual Studio 2017 and Microsoft Visual Studio Community 2017 are referred to as *Visual Studio* throughout this tutorial series.</span></span>

* <span data-ttu-id="ce789-201">Visual Studio 2017 je nainstalováno vedle všech starších verzí, které jsou již nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="ce789-201">Visual Studio 2017 is installed next to any older versions already installed.</span></span> <span data-ttu-id="ce789-202">Weby vytvořené v dřívějších verzích lze otevřít v aplikaci Visual Studio 2017 a nadále otevírat v předchozích verzích.</span><span class="sxs-lookup"><span data-stu-id="ce789-202">Sites created in earlier versions can be opened in Visual Studio 2017 and continue to open in previous versions.</span></span>

* <span data-ttu-id="ce789-203">Při prvním spuštění sady Visual Studio se předpokládá, že jste vybrali nastavení *vývoje webu* .</span><span class="sxs-lookup"><span data-stu-id="ce789-203">The first time you started Visual Studio, it is assumed you selected the *Web Development* settings.</span></span> <span data-ttu-id="ce789-204">Další informace najdete v tématu [Postupy: výběr nastavení prostředí pro vývoj webu](https://msdn.microsoft.com/library/ff521558.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce789-204">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

<span data-ttu-id="ce789-205">Po instalaci požadovaných součástí jste připraveni začít vytvářet webový projekt prezentovaný v této sérii kurzů.</span><span class="sxs-lookup"><span data-stu-id="ce789-205">After installing the prerequisites, you're ready to begin creating the Web project presented in this tutorial series.</span></span>

## <a name="download-the-sample-application"></a><span data-ttu-id="ce789-206">Stažení ukázkové aplikace</span><span class="sxs-lookup"><span data-stu-id="ce789-206">Download the sample application</span></span>

 <span data-ttu-id="ce789-207">Dokončenou ukázkovou aplikaci si můžete kdykoli stáhnout z webu ukázek na webu MSDN:</span><span class="sxs-lookup"><span data-stu-id="ce789-207">You can download the completed sample application at anytime from the MSDN Samples site:</span></span>

<span data-ttu-id="ce789-208">[Začínáme s webovými formuláři ASP.NET 4,5 a Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="ce789-208">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

 <span data-ttu-id="ce789-209">Tento soubor ke stažení obsahuje následující položky:</span><span class="sxs-lookup"><span data-stu-id="ce789-209">This download has the following items:</span></span>

- <span data-ttu-id="ce789-210">Ukázková aplikace ve složce *WingtipToys*</span><span class="sxs-lookup"><span data-stu-id="ce789-210">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="ce789-211">Prostředky použité k vytvoření ukázkové aplikace ve složce *WingtipToys-assets* ve složce *WingtipToys*</span><span class="sxs-lookup"><span data-stu-id="ce789-211">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

<span data-ttu-id="ce789-212">Soubor ke stažení je soubor *. zip* .</span><span class="sxs-lookup"><span data-stu-id="ce789-212">The download is a *.zip* file.</span></span> <span data-ttu-id="ce789-213">Pokud chcete zobrazit dokončený projekt, který tato série kurzů vytvoří, najděte a *C#* vyberte složku v souboru. zip.</span><span class="sxs-lookup"><span data-stu-id="ce789-213">To see the completed project that this tutorial series creates, find and select the *C#* folder in the .zip file.</span></span> <span data-ttu-id="ce789-214">Uložte C# složku do složky, kterou používáte pro práci s projekty aplikace Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce789-214">Save the C# folder to the folder you use to work with Visual Studio projects.</span></span> <span data-ttu-id="ce789-215">Ve výchozím nastavení je složka projektů sady Visual Studio 2017:</span><span class="sxs-lookup"><span data-stu-id="ce789-215">By default, the Visual Studio 2017 projects folder is:</span></span>

<span data-ttu-id="ce789-216"><strong>C:\Users&#92;</strong>  <strong><em>&lt;username&gt;</em></strong> <strong>\source\repos</strong></span><span class="sxs-lookup"><span data-stu-id="ce789-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span></span>

<span data-ttu-id="ce789-217">Přejmenujte ***C#*** složku na ***WingtipToys***.</span><span class="sxs-lookup"><span data-stu-id="ce789-217">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="ce789-218">Pokud ve složce Projects již máte složku s názvem *WingtipToys* , před přejmenováním *C#* složky na *WingtipToys*tuto existující složku dočasně přejmenujte.</span><span class="sxs-lookup"><span data-stu-id="ce789-218">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>

<span data-ttu-id="ce789-219">Chcete-li spustit dokončený projekt, otevřete složku *WingtipToys* a dvakrát klikněte na soubor *WingtipToys. sln* .</span><span class="sxs-lookup"><span data-stu-id="ce789-219">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="ce789-220">Visual Studio 2017 otevře projekt.</span><span class="sxs-lookup"><span data-stu-id="ce789-220">Visual Studio 2017 opens the project.</span></span> <span data-ttu-id="ce789-221">Potom klikněte pravým tlačítkem myši na soubor *Default. aspx* v **Průzkumník řešení** a vyberte možnost **Zobrazit v prohlížeči**.</span><span class="sxs-lookup"><span data-stu-id="ce789-221">Next, right-click the *Default.aspx* file in **Solution Explorer** and select **View In Browser**.</span></span>

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a><span data-ttu-id="ce789-222">Vytvoření kvízu webových formulářů ASP.NET pro kontrolu obsahu</span><span class="sxs-lookup"><span data-stu-id="ce789-222">Take a ASP.NET Web Forms quiz to review content</span></span>

<span data-ttu-id="ce789-223">Po dokončení série kurzů si požádejte kvíz o testování znalostí a posílení klíčových konceptů.</span><span class="sxs-lookup"><span data-stu-id="ce789-223">After completing the tutorial series, take a quiz to test your knowledge and reinforce key concepts.</span></span> <span data-ttu-id="ce789-224">Každá otázka obsahuje vysvětlení a odkazy na další doprovodné materiály.</span><span class="sxs-lookup"><span data-stu-id="ce789-224">Each question provides an explanation and links to additional guidance.</span></span>

* [<span data-ttu-id="ce789-225">Kvíz webových formulářů ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ce789-225">ASP.NET Web Forms Quiz</span></span>](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a><span data-ttu-id="ce789-226">Kurzová podpora a komentáře</span><span class="sxs-lookup"><span data-stu-id="ce789-226">Tutorial support and comments</span></span>

<span data-ttu-id="ce789-227">V případě otázek a komentářů použijte část Q a část, která je součástí [Začínáme s webovými formuláři ASP.NET 4,5 a Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) s ukázkovou stránkou.</span><span class="sxs-lookup"><span data-stu-id="ce789-227">For questions and comments, use the Q and A section included on the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span>

<span data-ttu-id="ce789-228">Komentáře k této sérii kurzů jsou Vítá vás.</span><span class="sxs-lookup"><span data-stu-id="ce789-228">Comments on this tutorial series are welcome.</span></span> <span data-ttu-id="ce789-229">Po aktualizaci této série kurzů se provede každé úsilí, aby se zohlednily opravy nebo návrhy na vylepšení.</span><span class="sxs-lookup"><span data-stu-id="ce789-229">When this tutorial series is updated, every effort is made to consider corrections or suggestions for improvements.</span></span>

<span data-ttu-id="ce789-230">Pokud dojde k chybě, mohou být příslušné chybové zprávy matoucí, a to bez vhodného vysvětlení, jak je opravit.</span><span class="sxs-lookup"><span data-stu-id="ce789-230">If an error occurs, the corresponding error messages could be confusing, with no good explanation on how to fix it.</span></span> <span data-ttu-id="ce789-231">Nápovědu můžete vyhledat ve [fórech ASP.NET](https://forums.asp.net/).</span><span class="sxs-lookup"><span data-stu-id="ce789-231">For help, you can check the [ASP.NET forums](https://forums.asp.net/).</span></span> <span data-ttu-id="ce789-232">Dalším dobrým zdrojem je oddíl Q a a ve [Začínáme s webovými formuláři ASP.NET 4,5 a na ukázkové stránce Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#).</span><span class="sxs-lookup"><span data-stu-id="ce789-232">Another good source is the Q and A section in the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="ce789-233">Next</span><span class="sxs-lookup"><span data-stu-id="ce789-233">Next</span></span>](create-the-project.md)
