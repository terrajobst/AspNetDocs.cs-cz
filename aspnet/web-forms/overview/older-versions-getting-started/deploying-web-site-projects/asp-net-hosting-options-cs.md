---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-cs
title: Technologie ASP.NET, který je hostitelem – možnosti (C#) | Dokumentace Microsoftu
author: rick-anderson
description: Webové aplikace ASP.NET jsou obvykle navrženy, vytvořili a otestovat v místním vývojovém prostředí a musí být nasazeny produkčního prostředí o...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 89a1d2bc-fdfd-4c5c-a3b0-49a08baaf63a
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-cs
msc.type: authoredcontent
ms.openlocfilehash: 3adad579c5893fb4f40e7043b9ece78740080f65
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077077"
---
<a name="aspnet-hosting-options-c"></a><span data-ttu-id="d5508-103">Možnosti hostování v technologii ASP.NET (C#)</span><span class="sxs-lookup"><span data-stu-id="d5508-103">ASP.NET Hosting Options (C#)</span></span>
====================
<span data-ttu-id="d5508-104">podle [Scott Meisnerová](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="d5508-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

[<span data-ttu-id="d5508-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="d5508-105">Download PDF</span></span>](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial01_Basics_cs.pdf)

> <span data-ttu-id="d5508-106">Webové aplikace ASP.NET jsou obvykle navržené, vytvořit a otestovat v místním vývojovém prostředí a potřebujete k nasazení do produkčního prostředí, až bude připravená pro vydanou verzi.</span><span class="sxs-lookup"><span data-stu-id="d5508-106">ASP.NET web applications are typically designed, created, and tested in a local development environment and need to be deployed to a production environment once it is ready for release.</span></span> <span data-ttu-id="d5508-107">Tento kurz poskytuje základní přehled o procesu nasazení a slouží jako úvod k této sérii kurzů.</span><span class="sxs-lookup"><span data-stu-id="d5508-107">This tutorial provides a high-level overview of the deployment process and serves as an introduction to this tutorial series.</span></span>


## <a name="introduction"></a><span data-ttu-id="d5508-108">Úvod</span><span class="sxs-lookup"><span data-stu-id="d5508-108">Introduction</span></span>

<span data-ttu-id="d5508-109">Webové aplikace jsou obvykle navrženy, vytvořili a testovat v prostředí pro vývoj, který je přístupný pouze pro programátory práce na webu.</span><span class="sxs-lookup"><span data-stu-id="d5508-109">Web applications are typically designed, created, and tested in a development environment that is accessible only to the programmers working on the site.</span></span> <span data-ttu-id="d5508-110">Když aplikace je připravená uvolnit, se přesune do produkčního prostředí kde webu je přístupný všem uživatelům Internetu.</span><span class="sxs-lookup"><span data-stu-id="d5508-110">Once the application is ready to be released, it is moved to a production environment where the site can be accessed by anyone on the Internet.</span></span> <span data-ttu-id="d5508-111">Tento proces nasazení představuje určité problémy:</span><span class="sxs-lookup"><span data-stu-id="d5508-111">This deployment process introduces a number of challenges:</span></span>

- <span data-ttu-id="d5508-112">Musí existovat a být správně nastaveny, předtím, než je možné nasadit aplikaci ASP.NET; produkčním prostředí Kromě toho produkčního prostředí se musí zajistit aktuální s nejnovějšími opravami zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="d5508-112">A production environment must exist and be properly setup before an ASP.NET application can be deployed; moreover, the production environment must be kept up to date with the latest security patches.</span></span>
- <span data-ttu-id="d5508-113">Správnou sadu souborů značek, soubory kódu a podpůrné soubory musí být zkopírován z vývojového prostředí do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-113">The correct set of markup files, code files, and support files must be copied from the development environment to the production environment.</span></span> <span data-ttu-id="d5508-114">Pro datově řízené aplikace to může vyžadovat kopírování schéma databáze nebo data, při selhání.</span><span class="sxs-lookup"><span data-stu-id="d5508-114">For data-driven applications, this might require copying the database schema and/or data, as well.</span></span>
- <span data-ttu-id="d5508-115">Mohou existovat rozdíly mezi těmito dvěma prostředími konfigurací.</span><span class="sxs-lookup"><span data-stu-id="d5508-115">There may be configuration differences between the two environments.</span></span> <span data-ttu-id="d5508-116">Připojovací řetězec nebo e-mailu serveru databáze používá ve vývojovém prostředí budou pravděpodobně lišit od produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-116">The database connection string or email server used in the development environment will likely be different than the production environment.</span></span> <span data-ttu-id="d5508-117">A co víc chování aplikace může záviset na prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-117">What's more, the behavior of the application may depend on the environment.</span></span> <span data-ttu-id="d5508-118">Například při výskytu chyby ve vývoji podrobnosti o chybě lze zobrazit na obrazovce, ale v případě chyby v produkčním prostředí by měl být místo toho zobrazen uživatelsky přívětivou chybovou stránku a podrobnosti o chybě e-mailem pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="d5508-118">For example, when an error occurs in development the error's details can be displayed on screen, but when an error occurs in production, a user-friendly error page should be displayed instead, and the error details emailed to the developers.</span></span>

<span data-ttu-id="d5508-119">Aby se předešlo první před obrovskou výzvou – nastavení a udržování produkčního prostředí – mnoho jednotlivců a podniků externí pomocí svých produkčních prostředích k *webové poskytovatelé hostingu*.</span><span class="sxs-lookup"><span data-stu-id="d5508-119">To obviate the first challenge - setting up and maintaining a production environment - many individuals and businesses outsource their production environments to *web hosting providers*.</span></span> <span data-ttu-id="d5508-120">Poskytovatele webových hostitelských služeb je společnost, která spravuje v provozním prostředí vaším jménem.</span><span class="sxs-lookup"><span data-stu-id="d5508-120">A web hosting provider is a company that manages the production environment on your behalf.</span></span> <span data-ttu-id="d5508-121">Existují aplikací webového hostitele zprostředkovatele, každý s různou cen a úrovní služeb; v části "Hledání hostiteli poskytovatele webových" tipy týkající se vyhledání poskytovatele služeb.</span><span class="sxs-lookup"><span data-stu-id="d5508-121">There are countless web host providers, each with varying prices and service levels; see the "Finding a Web Host Provider" section for tips on locating such a service provider.</span></span>

<span data-ttu-id="d5508-122">Toto je první ze série kurzů, které podívejte se na postup nasazení webové aplikace ASP.NET do produkčního prostředí spravované poskytovatelem webového hostitele.</span><span class="sxs-lookup"><span data-stu-id="d5508-122">This is the first in a series of tutorials that look at the steps involved in deploying an ASP.NET web application to a production environment managed by a web host provider.</span></span> <span data-ttu-id="d5508-123">V průběhu těchto kurzů prozkoumáme:</span><span class="sxs-lookup"><span data-stu-id="d5508-123">Over the course of these tutorials we will examine:</span></span>

- <span data-ttu-id="d5508-124">Jaké soubory je potřeba nasadit ke zprostředkovateli webového hostitele.</span><span class="sxs-lookup"><span data-stu-id="d5508-124">What files need to be deployed to the web host provider.</span></span>
- <span data-ttu-id="d5508-125">Nástroje pro zjednodušení procesu nasazení.</span><span class="sxs-lookup"><span data-stu-id="d5508-125">Tools for streamlining the deployment process.</span></span>
- <span data-ttu-id="d5508-126">Postup nasazení databáze.</span><span class="sxs-lookup"><span data-stu-id="d5508-126">How to deploy a database.</span></span>
- <span data-ttu-id="d5508-127">Tipy pro nasazení, která používá databázi [zprostředkovatele SQL na základě členství a rolí](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md), stejně jako se způsoby tak, aby napodoboval nástroje pro správu webu v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-127">Tips for deploying a database that uses [the SQL-based Membership and Roles provider](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md), along with ways to mimic the Website Administration Tool in a production environment.</span></span>
- <span data-ttu-id="d5508-128">Strategie pro plynule aktualizace databáze v produkčním prostředí se změnami provedenými během vývoje.</span><span class="sxs-lookup"><span data-stu-id="d5508-128">Strategies for smoothly updating the database in production with changes made during development.</span></span>
- <span data-ttu-id="d5508-129">Techniky pro protokolování chyb, ke kterým dochází v produkčním prostředí a způsoby, jak upozornit vývojáře, dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="d5508-129">Techniques for logging errors that occur on production, and ways to notify developers when an error occurs.</span></span>

<span data-ttu-id="d5508-130">Tyto kurzy jsou zaměřené stručné a poskytují podrobné pokyny s dostatečným snímky obrazovky, který vás provede procesem vizuálně.</span><span class="sxs-lookup"><span data-stu-id="d5508-130">These tutorials are geared to be concise and to provide step-by-step instructions with plenty of screen shots to walk you through the process visually.</span></span> <span data-ttu-id="d5508-131">V tomto kurzu zahajovací poskytuje přehled o procesu nasazení technologie ASP.NET a Rady, jak na hledání na webu poskytovatele hostitelských služeb.</span><span class="sxs-lookup"><span data-stu-id="d5508-131">This inaugural tutorial provides an overview of the ASP.NET deployment process and advice on finding a web hosting provider.</span></span> <span data-ttu-id="d5508-132">Pusťme se do práce!</span><span class="sxs-lookup"><span data-stu-id="d5508-132">Let's get started!</span></span>

## <a name="an-overview-of-the-aspnet-deployment-process"></a><span data-ttu-id="d5508-133">Přehled procesu nasazení technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d5508-133">An Overview of the ASP.NET Deployment Process</span></span>

<span data-ttu-id="d5508-134">Řečeno v kostce nasazení aplikace ASP.NET zahrnuje následující tři kroky:</span><span class="sxs-lookup"><span data-stu-id="d5508-134">In a nutshell, deploying an ASP.NET application involves the following three steps:</span></span>

1. <span data-ttu-id="d5508-135">Konfigurace webové aplikace, webový server a databáze v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-135">Configure the web application, web server, and database in the production environment.</span></span>
2. <span data-ttu-id="d5508-136">Synchronizovat stránek ASP.NET, soubory kódu, sestavení v `Bin` složky a související s HTML podpůrné soubory, jako jsou soubory šablon stylů CSS a JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="d5508-136">Synchronize the ASP.NET pages, code files, the assemblies in the `Bin` folder, and HTML-related support files like CSS and JavaScript files.</span></span>
3. <span data-ttu-id="d5508-137">Synchronizujte schéma databáze nebo data.</span><span class="sxs-lookup"><span data-stu-id="d5508-137">Synchronize the database schema and/or data.</span></span>

<span data-ttu-id="d5508-138">Informace o konfiguraci pro webovou aplikaci se obvykle nachází v `Web.config` souboru a obsahuje databázové připojovací řetězce, zpracování chyb kritéria přepsání pravidel a informace o serveru e-mailovou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="d5508-138">The configuration information for a web application is typically located in the `Web.config` file, and includes database connection strings, error handling criteria, URL rewriting rules, and email server information.</span></span> <span data-ttu-id="d5508-139">Tyto informace se často liší pro aplikace ve vývoji a stejné aplikace v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-139">Oftentimes this information is different for an application in development versus the same application in production.</span></span> <span data-ttu-id="d5508-140">Například při vývoji aplikace je nejvhodnější použít databázi vývoje tak, že nejsou testy na produkční databázi.</span><span class="sxs-lookup"><span data-stu-id="d5508-140">For instance, when developing an application it's best to use a development database so that you're not testing against the production database.</span></span> <span data-ttu-id="d5508-141">V důsledku toho připojovací řetězce databáze obvykle lišit mezi vývojovou a provozní aplikace.</span><span class="sxs-lookup"><span data-stu-id="d5508-141">As a result, the database connection strings typically differ between development and production applications.</span></span> <span data-ttu-id="d5508-142">Kvůli těmto rozdílům zahrnuje nasazování změn informace o konfiguraci webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="d5508-142">Due to these differences, part of deployment involves making changes to the web application's configuration information.</span></span>

<span data-ttu-id="d5508-143">Kromě změny konfigurace webové aplikace krok 1 také může mít za následek konfigurace pro webový server a databáze.</span><span class="sxs-lookup"><span data-stu-id="d5508-143">In addition to web application configuration changes, Step 1 also may entail configuration for the web server and database.</span></span> <span data-ttu-id="d5508-144">Například pokud stránky ASP.NET vytvoří nebo odstraní soubory z adresáře na webovém serveru pak webový server je potřeba nakonfigurovat tak, aby povolovala tyto úpravy systému souborů.</span><span class="sxs-lookup"><span data-stu-id="d5508-144">For example, if an ASP.NET page creates or deletes files from a directory on the web server then the web server needs to be configured to permit these file system modifications.</span></span> <span data-ttu-id="d5508-145">Podobně mohou být oprávnění nebo nastavení ověření, které je potřeba provést k databázi.</span><span class="sxs-lookup"><span data-stu-id="d5508-145">Similarly, there may be permission or authentication settings that need to be made to the database.</span></span>


<span data-ttu-id="d5508-146">Krok 2 zahrnuje synchronizaci sady základní stránky technologie ASP.NET a podpůrné soubory mezi vývojovou a provozní prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-146">Step 2 involves synchronizing the set of essential ASP.NET pages and support files between the development and production environments.</span></span> <span data-ttu-id="d5508-147">Konkrétní sada ASP. NET související soubory, které je třeba se dá provést synchronizace mezi těmito dvěma prostředími závisí na typu projektu vytvořené v sadě Visual Studio a je diskuze v dalším kurzu [ *určující, co soubory musí být nasazeny*](determining-what-files-need-to-be-deployed-cs.md).</span><span class="sxs-lookup"><span data-stu-id="d5508-147">The particular set of ASP.NET-related files that need to be synchronized between the two environments depends on the type of project you created in Visual Studio, and is the discussion in the next tutorial, [*Determining What Files Need to Be Deployed*](determining-what-files-need-to-be-deployed-cs.md).</span></span> <span data-ttu-id="d5508-148">Třetí a čtvrtá kurzy - [ *nasazení vašeho webu pomocí protokolu FTP* ](deploying-your-site-using-an-ftp-client-cs.md) a [ *nasazení webu pomocí sady Visual Studio* ](deploying-your-site-using-visual-studio-cs.md) – prozkoumejte různé nástroje a techniky pro synchronizaci těchto souborů.</span><span class="sxs-lookup"><span data-stu-id="d5508-148">The third and fourth tutorials - [*Deploying Your Site Using FTP*](deploying-your-site-using-an-ftp-client-cs.md) and [*Deploying Your Site Using Visual Studio*](deploying-your-site-using-visual-studio-cs.md) - examine different tools and techniques for syncing these files.</span></span>

<span data-ttu-id="d5508-149">Při sestavování aplikací řízených daty jsou obvykle dvě databáze používá: jeden pro vývoj a jeden v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-149">When building data-driven applications there are typically two databases being used: one for development and one on production.</span></span> <span data-ttu-id="d5508-150">Během vývoje schéma databáze vývoje může upravit tak, aby zahrnout nové tabulky, sloupce, uložené procedury a triggery nebo mohou být upraveny odebrat nebo přejmenovat stávající databázové objekty.</span><span class="sxs-lookup"><span data-stu-id="d5508-150">During development, the development database's schema may be modified to include new tables, columns, stored procedures, and triggers, or may be modified to remove or rename existing database objects.</span></span> <span data-ttu-id="d5508-151">Mezi časem, které budou provedeny tyto změny a čas, kdy aplikace je nasazená do produkčního prostředí nejsou synchronizované, vývoje a provozu databáze. Tato asynchronie je potřeba opravit během procesu nasazení.</span><span class="sxs-lookup"><span data-stu-id="d5508-151">Between the time that these changes are made and the time the application is deployed to production, the development and production databases are out of sync. This asynchrony needs to be fixed during the deployment process.</span></span> <span data-ttu-id="d5508-152">Tyto problémy se dají prozkoumat v budoucích kurzech.</span><span class="sxs-lookup"><span data-stu-id="d5508-152">These challenges will be examined in future tutorials.</span></span>

## <a name="finding-a-web-host-provider"></a><span data-ttu-id="d5508-153">Hledání zprostředkovateli webového hostitele</span><span class="sxs-lookup"><span data-stu-id="d5508-153">Finding a Web Host Provider</span></span>

<span data-ttu-id="d5508-154">Aplikace ASP.NET je nasadit na jakékoli webové servery, který má rozhraní .NET Framework a Internetové informační služby (IIS).</span><span class="sxs-lookup"><span data-stu-id="d5508-154">ASP.NET applications can be deployed to any web server that has the .NET Framework and Internet Information Services (IIS) installed.</span></span> <span data-ttu-id="d5508-155">Může hostovat lokalitu z počítače, za předpokladu, že jste měli širokopásmové připojení k Internetu a Přehled konfigurace směrovače pro povolení příchozích webových požadavků.</span><span class="sxs-lookup"><span data-stu-id="d5508-155">You could host a site from your personal computer, assuming you had a broadband connection to the Internet and the know how to configure your router to allow incoming web requests.</span></span> <span data-ttu-id="d5508-156">Může také hostujete lokality z počítače v intranetu, stejně jako mnoho společností.</span><span class="sxs-lookup"><span data-stu-id="d5508-156">You could also host a site from a computer in an intranet, as many companies do.</span></span> <span data-ttu-id="d5508-157">Zaměření pro tyto kurzy, ale je hostitelem vašeho webu pomocí zprostředkovatele webového hostitele.</span><span class="sxs-lookup"><span data-stu-id="d5508-157">The focus of these tutorials, however, is hosting your website with a web host provider.</span></span>

> [!NOTE]
> <span data-ttu-id="d5508-158">[Služba IIS](https://www.iis.net/) je webový server od Microsoftu na podnikové úrovni.</span><span class="sxs-lookup"><span data-stu-id="d5508-158">[IIS](https://www.iis.net/) is Microsoft's enterprise-grade web server.</span></span> <span data-ttu-id="d5508-159">Je dodáván s – Domovská stránka edice systému Windows, jako je například Windows Server 2008 a určitými edicemi systému Windows Vista.</span><span class="sxs-lookup"><span data-stu-id="d5508-159">It ships with the non-Home editions of Windows, such as Windows Server 2008 and certain editions of Windows Vista.</span></span> <span data-ttu-id="d5508-160">Instalace služby IIS k obsluze aplikace ASP.NET ve vývojovém prostředí sady Visual Studio obsahuje webový Server ASP.NET Development nepotřebujete.</span><span class="sxs-lookup"><span data-stu-id="d5508-160">You do not need to install IIS to serve ASP.NET applications in a development environment, as Visual Studio includes the ASP.NET Development Web Server.</span></span> <span data-ttu-id="d5508-161">Webový Server ASP.NET Development však přijímá pouze místní připojení a proto jej nelze použít v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-161">However, the ASP.NET Development Web Server only accepts local connections and therefore cannot be used in a production environment.</span></span>


<span data-ttu-id="d5508-162">Před nasazením webu poskytovatele webového hostitele je nutné rozhodnout údaje, které společnost uzavírat obchody se.</span><span class="sxs-lookup"><span data-stu-id="d5508-162">Before you can deploy your site to a web host provider you must first decide what company to do business with.</span></span> <span data-ttu-id="d5508-163">Existuje bezpočet webhosting společností ve službě na webu marketplace. Vyhledejte "webhosting společnosti" vrátí více než 5 milionů výsledky.</span><span class="sxs-lookup"><span data-stu-id="d5508-163">There are countless web hosting companies in the marketplace; a search for "web hosting company" returns more than five million results.</span></span> <span data-ttu-id="d5508-164">Jak najít ten, který je pro vás nejvhodnější?</span><span class="sxs-lookup"><span data-stu-id="d5508-164">How do you find the one that's right for you?</span></span> <span data-ttu-id="d5508-165">Váš oblíbený vyhledávací web není dobrý výchozí bod, protože jsou z webových, jako jsou [TopHosts](http://www.tophosts.com/) a [HostCritique](http://www.hostcritique.net/), který porovnání a kontrast různých hostitelských služeb.</span><span class="sxs-lookup"><span data-stu-id="d5508-165">Your favorite search engine is a good starting place, as are websites like [TopHosts](http://www.tophosts.com/) and [HostCritique](http://www.hostcritique.net/), which compare and contrast various hosting services.</span></span> <span data-ttu-id="d5508-166">Jsem také seznámit s kolegy a spolupracovníky žádostí o všechna doporučení; Můžete také požádat o doporučení v [hostování otevřené fórum](https://forums.asp.net/158.aspx) tady na [fóra ASP.NET](https://forums.asp.net/).</span><span class="sxs-lookup"><span data-stu-id="d5508-166">I also advise asking your colleagues and coworkers for any recommendations; you can also ask for recommendations at the [Hosting Open Forum](https://forums.asp.net/158.aspx) here at the [ASP.NET Forums](https://forums.asp.net/).</span></span>

<span data-ttu-id="d5508-167">Webové hostingové společnosti obvykle nabízejí sdílené plány hostování a vyhrazené plány hostování.</span><span class="sxs-lookup"><span data-stu-id="d5508-167">Web hosting companies typically offer shared hosting plans and dedicated hosting plans.</span></span> <span data-ttu-id="d5508-168">Pomocí sdílené hostování jediném webovém serveru hostitele desítky, pokud není stovky různých webů.</span><span class="sxs-lookup"><span data-stu-id="d5508-168">With shared hosting a single web server hosts dozens if not hundreds of different websites.</span></span> <span data-ttu-id="d5508-169">S vyhrazený hosting zapůjčení počítač ze společnosti, která slouží pouze váš web a Web.</span><span class="sxs-lookup"><span data-stu-id="d5508-169">With dedicated hosting you lease a computer from the company that serves your site and your site alone.</span></span> <span data-ttu-id="d5508-170">Sdílený plán hostování může zahrnují podporu pro stránky ASP.NET umožňuje pracovat s databází Microsoft Access, 5 GB místa na disku a 100 GB měsíčního výstupního provozu šířky pásma pro 9.95 $ za měsíc.</span><span class="sxs-lookup"><span data-stu-id="d5508-170">A shared hosting plan might include support for ASP.NET pages, the ability to work with Microsoft Access databases, 5 GB of disk space, and 100 GB of monthly bandwidth traffic for $9.95 per month.</span></span> <span data-ttu-id="d5508-171">Jiný sdílený plán hostování může zahrnují podporu pro stránky ASP.NET, přístup k databázi serveru Microsoft SQL Server 2008, 10 GB místa na disku a 250 GB měsíčního výstupního provozu šířky pásma pro 19,95 USD za měsíc.</span><span class="sxs-lookup"><span data-stu-id="d5508-171">Another shared hosting plan might include support for ASP.NET pages, access to the Microsoft SQL Server 2008 database server, 10 GB of disk space and 250 GB of monthly bandwidth traffic for $19.95 per month.</span></span> <span data-ttu-id="d5508-172">Vyhrazené plány hostování jsou obvykle mnohem dražší, ocenění několik stovek dolarů za měsíc, ale nabízejí lepší výkon a větší kontrolu, než sdílený možnosti hostování.</span><span class="sxs-lookup"><span data-stu-id="d5508-172">Dedicated hosting plans are usually much more expensive, costing several hundred dollars per month, but offer better performance and more control than shared hosting options.</span></span> <span data-ttu-id="d5508-173">Jaký plán zvolíte, závisí na rozpočtu, kolik provozu webu přijímá a funkce, které očekáváte, že je budete potřebovat.</span><span class="sxs-lookup"><span data-stu-id="d5508-173">What plan you choose depends on your budget, how much traffic your website receives, and the features you anticipate you'll need.</span></span>

<span data-ttu-id="d5508-174">Dva důležité aspekty při výběru poskytovatele webových hostitele jsou zákaznických služeb a kvalitu služeb.</span><span class="sxs-lookup"><span data-stu-id="d5508-174">Two important considerations when choosing a web host provider are customer service and quality of service.</span></span> <span data-ttu-id="d5508-175">Pokud máte dotazy nebo potíže s konfigurací, jak dlouho trvá v odesílání váš problém pro pracovníka webového hostitele, dokud získat odpověď?</span><span class="sxs-lookup"><span data-stu-id="d5508-175">If you have a question or a configuration problem, how long does it take from submitting your problem to the web host's helpdesk until you get a response?</span></span> <span data-ttu-id="d5508-176">Jak spolehlivé jsou služby vaší společnosti?</span><span class="sxs-lookup"><span data-stu-id="d5508-176">How reliable are the company's services?</span></span> <span data-ttu-id="d5508-177">Často mají výpadky databáze?</span><span class="sxs-lookup"><span data-stu-id="d5508-177">Do they frequently have database outages?</span></span> <span data-ttu-id="d5508-178">Jak často jejich e-mailový server přejdou do režimu offline?</span><span class="sxs-lookup"><span data-stu-id="d5508-178">How often does their email server go offline?</span></span> <span data-ttu-id="d5508-179">Můžete se vždy dotázat společnosti obsahují podrobné informace o jejich dostupnost a dotazovat se na svoje zásady služby zákazníka, ale více surefire způsob, jak se k vyžádání zpětné vazby z aktuálního i staršího zákazníků, které vám pomůžou prostřednictvím online fóra, diskusní skupiny a listservs e-mailu .</span><span class="sxs-lookup"><span data-stu-id="d5508-179">You can always ask a company to provide details about their uptime and inquire about their customer service policy, but a more surefire way is to solicit the feedback of current and past customers, which you can do through online forums, newsgroups, and email listservs.</span></span>

> [!NOTE]
> <span data-ttu-id="d5508-180">Některé webové hostingové společnosti soustředit svoje podnikání na konkrétní technologiích, jako je .NET nebo [LAMP](http://en.wikipedia.org/wiki/LAMP_stack) (**L** inux, **A** pache, **M** ySQL, a **P** HP), proto se ujistěte, že společnost vyberete hostuje aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d5508-180">Some web hosting companies focus their business on a particular technology stack, such as .NET or [LAMP](http://en.wikipedia.org/wiki/LAMP_stack) (**L** inux, **A** pache, **M** ySQL, and **P** HP), so make sure that the company you select hosts ASP.NET applications.</span></span> <span data-ttu-id="d5508-181">Také zkontrolujte, že podporují verzi technologie ASP.NET, který používáte k sestavení aplikace.</span><span class="sxs-lookup"><span data-stu-id="d5508-181">Also check to ensure that they support the version of ASP.NET you are using to build your application.</span></span> <span data-ttu-id="d5508-182">A pokud vytváříte aplikace řízené daty, ujistěte se, že nabízí webového hostitele na stejný server databáze a verze, kterou používáte.</span><span class="sxs-lookup"><span data-stu-id="d5508-182">And if you are building a data-driven application, make sure that the web host offers the same database server and version that you are using.</span></span>


## <a name="summary"></a><span data-ttu-id="d5508-183">Souhrn</span><span class="sxs-lookup"><span data-stu-id="d5508-183">Summary</span></span>

<span data-ttu-id="d5508-184">Webové aplikace ASP.NET jsou obvykle navržené, vytvořit a otestovat v místním vývojovém prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-184">ASP.NET web applications are typically designed, created, and tested in a local development environment.</span></span> <span data-ttu-id="d5508-185">Jakmile je připraven k vydání verze, se přesune do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="d5508-185">Once a version is ready for release, it is moved to a production environment.</span></span> <span data-ttu-id="d5508-186">I když je možné k hostování webů ASP.NET na váš osobní počítač nebo na serverech v rámci vaší společnosti, zvolte využívající hostování webového hostitele poskytovatele mnoho firmy i jednotlivce.</span><span class="sxs-lookup"><span data-stu-id="d5508-186">While it is possible to host ASP.NET websites on your personal computer or on servers within your company, many businesses and individuals choose to outsource their hosting to a web host provider.</span></span>

<span data-ttu-id="d5508-187">V této sérii kurzů prozkoumá postup nasazení aplikace ASP.NET u poskytovatele webových hostitele, zkoumání běžných problémů.</span><span class="sxs-lookup"><span data-stu-id="d5508-187">This tutorial series examines the steps for deploying an ASP.NET application to a web host provider, exploring common challenges.</span></span> <span data-ttu-id="d5508-188">Tento kurz nabízí přehled procesu nasazení technologie ASP.NET a dala tipy pro vyhledání vhodné webový poskytovatel hostitele.</span><span class="sxs-lookup"><span data-stu-id="d5508-188">This tutorial offered a high-level overview of the ASP.NET deployment process and gave tips for finding a suitable web host provider.</span></span> <span data-ttu-id="d5508-189">V dalším kurzu se prohledá co soubory související s ASP.NET je nutné zkopírovat do produkčního prostředí při nasazování webu.</span><span class="sxs-lookup"><span data-stu-id="d5508-189">The next tutorial looks at what ASP.NET-related files need to be copied to the production environment when deploying your website.</span></span>

<span data-ttu-id="d5508-190">Všechno nejlepší programování!</span><span class="sxs-lookup"><span data-stu-id="d5508-190">Happy Programming!</span></span>

### <a name="special-thanks-to"></a><span data-ttu-id="d5508-191">Speciální k...</span><span class="sxs-lookup"><span data-stu-id="d5508-191">Special Thanks To…</span></span>

<span data-ttu-id="d5508-192">V této sérii kurzů byl recenzován uživatelem mnoho užitečných revidující.</span><span class="sxs-lookup"><span data-stu-id="d5508-192">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="d5508-193">Vedoucí kontrolor pro účely tohoto kurzu byla Teresy Murphy.</span><span class="sxs-lookup"><span data-stu-id="d5508-193">Lead reviewer for this tutorial was Teresa Murphy.</span></span> <span data-ttu-id="d5508-194">Zajímat téma Moje nadcházejících článcích MSDN?</span><span class="sxs-lookup"><span data-stu-id="d5508-194">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="d5508-195">Pokud ano, vyřaďte mě řádek na [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com).</span><span class="sxs-lookup"><span data-stu-id="d5508-195">If so, drop me a line at [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d5508-196">Next</span><span class="sxs-lookup"><span data-stu-id="d5508-196">Next</span></span>](determining-what-files-need-to-be-deployed-cs.md)