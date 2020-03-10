---
uid: web-pages/readme/overview
title: Soubor Readme WebMatrix | Microsoft Docs
author: rick-anderson
description: Soubor Readme pro ASP.NET verze WebMatrix a Web Pages (Razor) 1,0
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563467"
---
# <a name="webmatrix-readme"></a><span data-ttu-id="f7a69-103">WebMatrix – soubor Readme</span><span class="sxs-lookup"><span data-stu-id="f7a69-103">WebMatrix Readme</span></span>

<span data-ttu-id="f7a69-104">13. ledna 2011</span><span class="sxs-lookup"><span data-stu-id="f7a69-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="f7a69-105">Obsah</span><span class="sxs-lookup"><span data-stu-id="f7a69-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="f7a69-106">Tento soubor Readme se týká verze 1,0 WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-106">This readme applies to the 1.0 release of WebMatrix.</span></span>

- [<span data-ttu-id="f7a69-107">Přehled</span><span class="sxs-lookup"><span data-stu-id="f7a69-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="f7a69-108">Instalace</span><span class="sxs-lookup"><span data-stu-id="f7a69-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="f7a69-109">Jak publikovat aplikace</span><span class="sxs-lookup"><span data-stu-id="f7a69-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="f7a69-110">Změny a problémy</span><span class="sxs-lookup"><span data-stu-id="f7a69-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="f7a69-111">Instalace WebMatrix 1,0</span><span class="sxs-lookup"><span data-stu-id="f7a69-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="f7a69-112">Webové stránky ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f7a69-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="f7a69-113">WebMatrixu</span><span class="sxs-lookup"><span data-stu-id="f7a69-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="f7a69-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="f7a69-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="f7a69-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="f7a69-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="f7a69-116">Instalace aplikací</span><span class="sxs-lookup"><span data-stu-id="f7a69-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="f7a69-117">Publikování aplikací</span><span class="sxs-lookup"><span data-stu-id="f7a69-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="f7a69-118">Další informace</span><span class="sxs-lookup"><span data-stu-id="f7a69-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="f7a69-119">Přehled</span><span class="sxs-lookup"><span data-stu-id="f7a69-119">Overview</span></span>

> <span data-ttu-id="f7a69-120">Microsoft WebMatrix 1,0 je bezplatný sada pro vývoj webů, která se instaluje během několika minut.</span><span class="sxs-lookup"><span data-stu-id="f7a69-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="f7a69-121">Integruje webový server s databázovými a programovacími rozhraními k vytvoření jediného integrovaného prostředí.</span><span class="sxs-lookup"><span data-stu-id="f7a69-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="f7a69-122">Pomocí WebMatrixu můžete zjednodušit způsob, jakým kód, otestujete a publikujete vlastní web ASP.NET nebo PHP, nebo můžete pomocí WebMatrixu začít nový web pomocí oblíbených open source aplikací, jako je DotNetNuke, Umbraco, WordPress nebo Joomla.</span><span class="sxs-lookup"><span data-stu-id="f7a69-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="f7a69-123">WebMatrix používá stejný výkonný prostředí webového serveru, databázového stroje a rozhraní, které spustí vaši webovou stránku na internetu, což usnadňuje přechod z vývoje do produkčního prostředí a hladkého a bezproblémového.</span><span class="sxs-lookup"><span data-stu-id="f7a69-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="f7a69-124">Instalace</span><span class="sxs-lookup"><span data-stu-id="f7a69-124">Installation</span></span>

> <span data-ttu-id="f7a69-125">Pokud chcete nainstalovat WebMatrix 1,0, musíte nejdřív nainstalovat [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="f7a69-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="f7a69-126">Po nainstalování instalačního programu webové platformy ho můžete použít k instalaci WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="f7a69-127">Pokud máte při instalaci problémy, přečtěte si téma [řešení potíží s instalace webové platformy Microsoft](https://go.microsoft.com/fwlink/?LinkId=196212).</span><span class="sxs-lookup"><span data-stu-id="f7a69-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="f7a69-128">Jak publikovat aplikace</span><span class="sxs-lookup"><span data-stu-id="f7a69-128">How to Publish Applications</span></span>

> <span data-ttu-id="f7a69-129">Přečtěte si podrobné [pokyny pro publikování aplikací](https://go.microsoft.com/fwlink/?LinkID=196149) .</span><span class="sxs-lookup"><span data-stu-id="f7a69-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="f7a69-130">Změny a problémy</span><span class="sxs-lookup"><span data-stu-id="f7a69-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="f7a69-131">Problémy s instalací WebMatrix 1,0</span><span class="sxs-lookup"><span data-stu-id="f7a69-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="f7a69-132">Problém: WebMatrix 1,0 je dostupný jenom na platformách, které podporují Microsoft .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="f7a69-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="f7a69-133">Pro WebMatrix se vyžaduje .NET Framework verze 4.</span><span class="sxs-lookup"><span data-stu-id="f7a69-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="f7a69-134">V některých případech se instalační program WebMatrix 1,0 pokusí nainstalovat na platformu, která není součástí podporované konfigurační sady.</span><span class="sxs-lookup"><span data-stu-id="f7a69-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="f7a69-135">Konkrétně Windows Vista bez aktualizace SP1 vám umožní zahájit instalaci WebMatrixu, ale komponenta .NET Framework 4 selže a zablokuje instalaci.</span><span class="sxs-lookup"><span data-stu-id="f7a69-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="f7a69-136">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-136">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-137">Nainstalujte na podporovanou platformu, která zahrnuje:</span><span class="sxs-lookup"><span data-stu-id="f7a69-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="f7a69-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="f7a69-138">Windows 7</span></span>
> - <span data-ttu-id="f7a69-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="f7a69-139">Windows Server 2008</span></span>
> - <span data-ttu-id="f7a69-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="f7a69-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="f7a69-141">Windows Vista SP1 nebo novější</span><span class="sxs-lookup"><span data-stu-id="f7a69-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="f7a69-142">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="f7a69-142">Windows XP SP3</span></span>
> - <span data-ttu-id="f7a69-143">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="f7a69-143">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="f7a69-144">Problém: nejde nainstalovat WebMatrix 1,0, pokud je nainstalovaná Microsoft Visual Studio 2008 bez Microsoft Visual Studio 2008 SP1.</span><span class="sxs-lookup"><span data-stu-id="f7a69-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="f7a69-145">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-145">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-146">Nainstalujte [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) z webu Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="f7a69-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="f7a69-147">Problém: některá sestavení pro SQL Server Compact 4,0 nejsou v globální mezipaměti sestavení (GAC) nainstalovaná.</span><span class="sxs-lookup"><span data-stu-id="f7a69-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="f7a69-148">Spravovaná sestavení pro SQL Server Compact 4,0 nejsou vložena do globální mezipaměti sestavení (GAC) při instalaci SQL Server Compact 4,0 na počítači 64 a počítač má nainstalovaný pouze klientský profil .NET Framework 3,5 SP1.</span><span class="sxs-lookup"><span data-stu-id="f7a69-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="f7a69-149">Spravovaná sestavení, která nejsou nainstalovaná v globální mezipaměti sestavení (GAC), jsou:</span><span class="sxs-lookup"><span data-stu-id="f7a69-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="f7a69-150">*System. data. SqlServerCe. dll* (poskytovatel ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="f7a69-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="f7a69-151">*System. data. SqlServerCe. entity. dll* (ADO.NET Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="f7a69-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="f7a69-152">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-152">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-153">Odinstalujte SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="f7a69-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="f7a69-154">Úplnou verzi .NET Framework 3,5 SP1 si stáhněte a nainstalujte z následujícího umístění:</span><span class="sxs-lookup"><span data-stu-id="f7a69-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="f7a69-155">Microsoft .NET Framework 3,5 Service Pack 1 (úplný balíček)</span><span class="sxs-lookup"><span data-stu-id="f7a69-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="f7a69-156">Pak přeinstalujte SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="f7a69-156">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="f7a69-157">Problém: SQL Server Compact nejde odinstalovat pomocí příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="f7a69-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="f7a69-158">Odinstalace SQL Server Compact pomocí možností příkazového řádku nefunguje v této verzi.</span><span class="sxs-lookup"><span data-stu-id="f7a69-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="f7a69-159">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-159">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-160">Pomocí *programů a funkcí* v Ovládacích panelech systému Windows odinstalujte Microsoft SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="f7a69-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="f7a69-161">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="f7a69-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="f7a69-162">Tato část dokumentu popisuje nové funkce, změny a známé problémy s verzí 1,0 webových stránek ASP.NET s využitím syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="f7a69-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="f7a69-163">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="f7a69-163">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="f7a69-164">Provedeny</span><span class="sxs-lookup"><span data-stu-id="f7a69-164">Changes</span></span>](#Changes)
- [<span data-ttu-id="f7a69-165">Problémy</span><span class="sxs-lookup"><span data-stu-id="f7a69-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a><span data-ttu-id="f7a69-166">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="f7a69-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="f7a69-167">Novinka: Přidání nastavení konfigurace za účelem zakázání správce balíčků</span><span class="sxs-lookup"><span data-stu-id="f7a69-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="f7a69-168">Nový klíč `asp:AdminManagerEnabled` je k dispozici pro `<appSettings>` prvek v souboru *Web. config* , který umožňuje zcela zakázat Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="f7a69-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="f7a69-169">Výchozí hodnota pro tento prvek je true, to znamená, že pokud není obsažena v souboru *Web. config* , je povolen správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="f7a69-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="f7a69-170">Chcete-li zakázat Správce balíčků, přidejte následující element do souboru *Web. config* v kořenovém adresáři webu:</span><span class="sxs-lookup"><span data-stu-id="f7a69-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a><span data-ttu-id="f7a69-171">Provedeny</span><span class="sxs-lookup"><span data-stu-id="f7a69-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="f7a69-172">Změna: klíč webpages: AdminFolderVirtualPath se přejmenoval na ASP: AdminFolderVirtualPath.</span><span class="sxs-lookup"><span data-stu-id="f7a69-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="f7a69-173">Klíč `webPages:AdminFolderVirtualPath`, který lze přidat do souboru *Web. config* pro určení umístění správce balíčků, byl přejmenován na použití `asp:`ho oboru názvů namísto oboru názvů `webPages`.</span><span class="sxs-lookup"><span data-stu-id="f7a69-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="f7a69-174">Pokud jste tento prvek použili, je nutné jej přejmenovat v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="f7a69-174">If you have used this element, you must rename it in the configuration file.</span></span>

#### <a id="Issues"></a> <span data-ttu-id="f7a69-175">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="f7a69-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="f7a69-176">Problém: hesla pro uživatele členství již nejsou rozpoznána.</span><span class="sxs-lookup"><span data-stu-id="f7a69-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="f7a69-177">Algoritmus pro vytváření a ukládání hesel členství (přihlášení) byl změněn tak, aby byl bezpečnější.</span><span class="sxs-lookup"><span data-stu-id="f7a69-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="f7a69-178">V důsledku toho nebudou rozpoznána hesla uložená pro členy (uživatelé) vytvořená ve verzích beta verze ASP.NET Razor.</span><span class="sxs-lookup"><span data-stu-id="f7a69-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="f7a69-179">**Alternativní řešení** Pokud lokalita ještě není vložená do produkčního prostředí, odeberte z databáze členství záznamy uživatelů.</span><span class="sxs-lookup"><span data-stu-id="f7a69-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="f7a69-180">Pokud je databáze živá, programově znovu vygenerujte stávající hesla v databázi členství.</span><span class="sxs-lookup"><span data-stu-id="f7a69-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="f7a69-181">Problém: neočekávané chování při použití vlastní uživatelské tabulky pro členství</span><span class="sxs-lookup"><span data-stu-id="f7a69-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="f7a69-182">Chcete-li inicializovat poskytovatele členství pro web ASP.NET Razor, zavoláte metodu `WebSecurity.InitializeDatabaseConnection`.</span><span class="sxs-lookup"><span data-stu-id="f7a69-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="f7a69-183">(Ve webové matici úvodní šablona webu obsahuje volání této metody v souboru *\_AppStart. cshtml* .) Pokud je parametr `autoCreateTables` této metody nastaven na hodnotu true (ve výchozím nastavení je nastaven na hodnotu true v šabloně počátečního webu) a pokud je do metody (druhý parametr) předána nerozpoznaný název tabulky, metoda nevyvolá chybu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="f7a69-184">Místo toho se tabulka automaticky vytvoří.</span><span class="sxs-lookup"><span data-stu-id="f7a69-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="f7a69-185">To může být problém, pokud máte v úmyslu použít pro členství vlastní uživatelskou tabulku, ale předat do metody `WebSecurity.InitializeDatabaseConnection` špatný název tabulky.</span><span class="sxs-lookup"><span data-stu-id="f7a69-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="f7a69-186">Vzhledem k tomu, že metoda není ve výchozím nastavení vyvolána, pokud zadaná tabulka neexistuje a protože místo toho vytvoří novou tabulku, aplikace může vypadat, že bude fungovat.</span><span class="sxs-lookup"><span data-stu-id="f7a69-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="f7a69-187">Nicméně kód aplikace, který závisí na vlastní uživatelské tabulce (a u polí v ní), může nakonec selhat s neočekávanými chybami.</span><span class="sxs-lookup"><span data-stu-id="f7a69-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="f7a69-188">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-188">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-189">Ujistěte se, že název předaný v metodě `InitializeDatabaseConnection` odpovídá tabulce profilů uživatele v databázi členství, nebo se ujistěte, že parametr `autoCreateTables` je nastaven na hodnotu false.</span><span class="sxs-lookup"><span data-stu-id="f7a69-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a><span data-ttu-id="f7a69-190">Problém: chybová zpráva "modul Správce vyžaduje přístup k ~/App\_data"</span><span class="sxs-lookup"><span data-stu-id="f7a69-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="f7a69-191">V některých případech se při pokusu o vytvoření uživatelů nebo jiné práci se systémem členství v ASP.NET může způsobit, že se na stránce zobrazí chyba *, že modul Správce vyžaduje přístup k ~/App\_data*.</span><span class="sxs-lookup"><span data-stu-id="f7a69-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="f7a69-192">K tomu dochází, pokud účet, na kterém je spuštěná služba IIS nebo IIS Express, nemá oprávnění k vytvoření a zápisu do složky *\_dat aplikace* v kořenovém adresáři webu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="f7a69-193">**Alternativní řešení** Ručně vytvořte složku *dat\_aplikace* pro web.</span><span class="sxs-lookup"><span data-stu-id="f7a69-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="f7a69-194">Pak se ujistěte, že účet systému Windows, pod kterým běží aplikace (obvykle síťová služba), má oprávnění ke čtení a zápisu pro kořenové složky aplikace a pro podsložky, jako jsou například data aplikace\_.</span><span class="sxs-lookup"><span data-stu-id="f7a69-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="f7a69-195">Podrobnější informace jsou k dispozici v článku znalostní báze [problémy s SQL Server Expressmi vytvářením uživatelských instancí a projektů webových aplikací ASP.NET](https://support.microsoft.com/kb/2002980).</span><span class="sxs-lookup"><span data-stu-id="f7a69-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="f7a69-196">Problém: nepovedlo se vygenerovat uživatelskou instanci SQL Server, chyba.</span><span class="sxs-lookup"><span data-stu-id="f7a69-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="f7a69-197">Pokud webová aplikace WebMatrix používá SQL Server Express a je v systému Windows 7 nebo Windows Server 2008 R2 spuštěna služba IIS 7,5, může se zobrazit chyba, která indikuje, že SQL Server během běhu nemůže načíst cestu k místní aplikaci uživatele.</span><span class="sxs-lookup"><span data-stu-id="f7a69-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="f7a69-198">**Alternativní řešení** Ujistěte se, že účet systému Windows, pod kterým je aplikace spuštěna (obvykle síťová služba), má oprávnění ke čtení a zápisu pro kořenové složky aplikace a pro podsložky, jako jsou například *data aplikace\_* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="f7a69-199">Podrobnější informace jsou k dispozici v článku znalostní báze [problémy s SQL Server Expressmi vytvářením uživatelských instancí a projektů webových aplikací ASP.NET](https://support.microsoft.com/kb/2002980).</span><span class="sxs-lookup"><span data-stu-id="f7a69-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="f7a69-200">Problém: soubory, které obsahují prostředky správce balíčků nebo hesla správce balíčků, jsou v rámci služby IIS 6,0 a starší.</span><span class="sxs-lookup"><span data-stu-id="f7a69-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="f7a69-201">Pokud nasadíte aplikaci ASP.NET Web Pages (Razor), která byla sestavena pomocí verze RC2, a pokud aplikace obsahuje soubor *Password. txt* nebo *packagesources. txt* v oblasti */App\_data/správce*, služba IIS 6,0 bude v případě potřeby využívat soubor a potenciálně vystaví hesla pro vaši instanci správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="f7a69-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="f7a69-202">**Alternativní řešení** Přejmenujte soubor *Password. txt* nebo *packagesources. txt* na *Password. config* nebo *packagesources. config*. Ve výchozím nastavení služba IIS 6,0 neposkytuje soubory, které mají příponu *. config* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="f7a69-203">(Ve službě IIS 7 se nezpracovávají žádné soubory ve složce *App\_data* , takže je nemusíte soubory přejmenovávat.)</span><span class="sxs-lookup"><span data-stu-id="f7a69-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="f7a69-204">Problém: odinstalování balíčků nainstalovaných pomocí beta 3 verze neodstraní zcela součásti balíčku.</span><span class="sxs-lookup"><span data-stu-id="f7a69-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="f7a69-205">Pokud jste balíček nainstalovali pomocí Správce balíčků ve verzi beta 3 a pak se pokusíte ho odinstalovat pomocí aktuální verze, balíček není zcela odinstalován.</span><span class="sxs-lookup"><span data-stu-id="f7a69-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="f7a69-206">Pomocí tlačítka **odinstalovat** správce balíčků se odstraní některé komponenty, ale ponechá kód knihovny balíčku a neaktualizuje soubor *Package. config* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="f7a69-207">**Alternativní řešení** </span><span class="sxs-lookup"><span data-stu-id="f7a69-207">**Workaround** </span></span>  
> <span data-ttu-id="f7a69-208">Proveďte tyto kroky:</span><span class="sxs-lookup"><span data-stu-id="f7a69-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="f7a69-209">Odstraňte složku *aplikace\_Data\packages* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="f7a69-210">Tím se odstraní všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="f7a69-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="f7a69-211">Odstraňte soubor *Packages. config* v kořenovém adresáři webu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-211">Delete the *packages.config* file in the root of the website.</span></span>

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="f7a69-212">Problém: v aplikaci Visual Studio vyvolání webového správce balíčků převede aplikaci do offline režimu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="f7a69-213">Pokud pracujete v aplikaci Visual Studio (nikoli WebMatrix) a ke spuštění Správce balíčků použijete funkci *\_admin* , Visual Studio převede aplikaci do offline režimu a odešle *aplikaci\_offline. htm* do kořenového adresáře webu, což narušuje možnosti použití Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="f7a69-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="f7a69-214">I když byste při použití webového rozhraní Správce balíčků nejčastěji viděli toto chování, dojde k stejnému chování, když přidáte, odeberete nebo upravíte jakékoli soubory ve složce *App\_data* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="f7a69-215">**Alternativní řešení** </span><span class="sxs-lookup"><span data-stu-id="f7a69-215">**Workaround** </span></span>  
> <span data-ttu-id="f7a69-216">Chcete-li pracovat s balíčky v aplikaci Visual Studio, použijte místo webového správce balíčků rozšíření NuGet.</span><span class="sxs-lookup"><span data-stu-id="f7a69-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="f7a69-217">Informace najdete v [dokumentaci k NuGet](https://docs.microsoft.com/nuget/).</span><span class="sxs-lookup"><span data-stu-id="f7a69-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="f7a69-218">Pokud pracujete s jinými soubory ve složce *App\_data* , zvažte, jestli soubory jsou jinde, abyste se tomuto problému vyhnuli.</span><span class="sxs-lookup"><span data-stu-id="f7a69-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="f7a69-219">Pokud to není praktické, odstraňte *aplikaci\_offline souboru. htm* ručně nebo počkejte, až se web automaticky vrátí do online režimu (ve výchozím nastavení po 30 sekundách).</span><span class="sxs-lookup"><span data-stu-id="f7a69-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="f7a69-220">Problém: Visual Studio IntelliSense a šablony projektů dostupné jenom ve ASP.NET MVC verze 3</span><span class="sxs-lookup"><span data-stu-id="f7a69-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="f7a69-221">Při instalaci webových stránek ASP.NET se také neinstalují nástroje pro Visual Studio, jako jsou IntelliSense a šablony projektů pro aplikace ASP.NET Web Pages.</span><span class="sxs-lookup"><span data-stu-id="f7a69-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="f7a69-222">**Alternativní řešení** Chcete-li používat IntelliSense a šablony projektů pro aplikace ASP.NET Web Pages v aplikaci Visual Studio, nainstalujte ASP.NET MVC 3 RC buď prostřednictvím instalačního programu webové platformy, nebo pomocí [samostatného instalačního programu](https://go.microsoft.com/fwlink/?LinkID=191797).</span><span class="sxs-lookup"><span data-stu-id="f7a69-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="f7a69-223">Problém: čtení informačních kanálů nebo jiných externích dat prostřednictvím proxy server</span><span class="sxs-lookup"><span data-stu-id="f7a69-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="f7a69-224">Pokud je server, na kterém je spuštěná lokalita, za proxy server, může být nutné nakonfigurovat informace o proxy serveru v souboru *Web. config* , aby bylo možné číst informace, které pocházejí z mimo vaši lokalitu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="f7a69-225">Pokud například použijete pomocníka `ReCaptcha`, pomáhající osoba komunikuje se službou reCAPTCHA, ale může být blokována proxy server.</span><span class="sxs-lookup"><span data-stu-id="f7a69-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="f7a69-226">Podobně kanály, které se používají v ASP.NET webové stránky, jako je informační kanál používaný správcem balíčků, můžou vyžadovat konfiguraci proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="f7a69-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="f7a69-227">Pokud dochází k potížím při práci s externí službou nebo při práci s kanálem balíčku, vložte následující prvky do kořenového souboru *Web. config* vaší aplikace:</span><span class="sxs-lookup"><span data-stu-id="f7a69-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="f7a69-228">Další informace o konfiguraci proxy server najdete v tématu [&lt;proxy&gt; elementu (nastavení sítě)](https://msdn.microsoft.com/library/sa91de1e.aspx) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="f7a69-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="f7a69-229">Problém: Odinstalace .NET Framework verze 4: zakáže webové stránky ASP.NET se syntaxí Razor.</span><span class="sxs-lookup"><span data-stu-id="f7a69-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="f7a69-230">Pokud odinstalujete .NET Framework verze 4 a pak ji znovu nainstalujete, ASP.NET webové stránky s syntaxe Razor jsou zakázané.</span><span class="sxs-lookup"><span data-stu-id="f7a69-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="f7a69-231">Stránky s příponou *. cshtml* neběží správně.</span><span class="sxs-lookup"><span data-stu-id="f7a69-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="f7a69-232">Webové stránky ASP.NET registrují sestavení v kořenovém souboru *Web. config* počítače a odebrání .NET Framework Tento soubor odebere.</span><span class="sxs-lookup"><span data-stu-id="f7a69-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="f7a69-233">Opětovná instalace .NET Framework nainstaluje novou verzi konfiguračního souboru, ale nepřidá odkaz pro sestavení webových stránek ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f7a69-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="f7a69-234">**Alternativní řešení** Po přeinstalaci .NET Framework přeinstalujte webové stránky ASP.NET pomocí syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="f7a69-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="f7a69-235">Tím se do souboru *Web. config* přidá následující element v kořenovém adresáři počítače, který je obvykle v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="f7a69-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="f7a69-236">Problém: adresy URL bez přípony nenaleznou soubory. cshtml/. vbhtml ve službě IIS 7 nebo IIS 7,5</span><span class="sxs-lookup"><span data-stu-id="f7a69-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="f7a69-237">V případě služby IIS 7 nebo IIS 7,5 nebudou žádosti s adresou URL, jako jsou následující, schopné najít stránky s příponou *. cshtml* nebo *. vbhtml* :</span><span class="sxs-lookup"><span data-stu-id="f7a69-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="f7a69-238">K tomuto problému dochází, protože přepis adres URL není ve výchozím nastavení povolený pro IIS 7 nebo IIS 7,5.</span><span class="sxs-lookup"><span data-stu-id="f7a69-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="f7a69-239">Ve scénáři likeliest se problém nezobrazuje při místním testování pomocí IIS Express, ale při nasazování webu na hostující web dojde k jeho práci.</span><span class="sxs-lookup"><span data-stu-id="f7a69-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="f7a69-240">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="f7a69-241">Pokud máte kontrolu nad počítačem serveru, na serverovém počítači nainstalujte aktualizaci popsanou v [aktualizaci, která umožňuje určitým obslužným rutinám služby iis 7,0 nebo iis 7,5 zpracovávat požadavky, jejichž adresy URL nekončí tečkou](https://support.microsoft.com/kb/980368).</span><span class="sxs-lookup"><span data-stu-id="f7a69-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="f7a69-242">Pokud nemáte kontrolu nad počítačem serveru (například nasazujete na hostující Web), přidejte následující do souboru *Web. config* webu:</span><span class="sxs-lookup"><span data-stu-id="f7a69-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="f7a69-243">Problém: nasazení aplikace do počítače, ve kterém není nainstalovaná SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="f7a69-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="f7a69-244">Aplikace, které zahrnují SQL Server Compact databáze, mohou běžet v počítači, kde není nainstalován SQL Server Compact.</span><span class="sxs-lookup"><span data-stu-id="f7a69-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="f7a69-245">Microsoft WebMatrix 1,0 automaticky zkopíruje tyto binární soubory a provede příslušné transformace souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="f7a69-246">**Alternativní řešení** Pokud potřebujete tyto soubory zkopírovat a provést změny v souboru *Web. config* ručně, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="f7a69-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="f7a69-247">Zkopírujte sestavení databázového stroje do složky *bin* (a podsložek) aplikace v cílovém počítači:</span><span class="sxs-lookup"><span data-stu-id="f7a69-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="f7a69-248">Kopírování *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span><span class="sxs-lookup"><span data-stu-id="f7a69-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>      <span data-ttu-id="f7a69-249">**do** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="f7a69-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="f7a69-250">Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **do** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="f7a69-250">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **to** *\Bin\x86*</span></span>
>    - <span data-ttu-id="f7a69-251">Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \* **do** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="f7a69-251">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 
> 2. <span data-ttu-id="f7a69-252">V kořenové složce webu vytvořte nebo otevřete soubor *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="f7a69-253">(Ve WebMatrixu 1,0 je tento typ souboru k dispozici, pokud kliknete na tlačítko **vše** v dialogovém okně **zvolit typ souboru** .)</span><span class="sxs-lookup"><span data-stu-id="f7a69-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="f7a69-254">Přidejte následující prvek jako podřízený prvek prvku `<configuration>` (není uvnitř elementu `<system.web>`):</span><span class="sxs-lookup"><span data-stu-id="f7a69-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="f7a69-255">Problém: pomocníka databáze a WebGrid nefungují v nestředním vztahu důvěryhodnosti v Visual Basic</span><span class="sxs-lookup"><span data-stu-id="f7a69-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="f7a69-256">Pokud používáte Visual Basic (vytváření souborů *. vbhtml* ), `Database` a `WebGrid` pomocníka nebudou fungovat, pokud je aplikace nastavená tak, aby používala střední důvěryhodnost.</span><span class="sxs-lookup"><span data-stu-id="f7a69-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="f7a69-257">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-257">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-258">Pokud používáte sadu Visual Studio 2010, můžete tento problém vyřešit instalací verze Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="f7a69-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="f7a69-259">Dokud nebude k dispozici konečná verze nástroje SP1, můžete stáhnout beta verzi nástroje SP1 ze stránky [Microsoft Visual Studio 2010 s aktualizací Service Pack 1 beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) na webu Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="f7a69-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="f7a69-260">Pokud to není praktické nebo pokud nepoužíváte sadu Visual Studio 2010, můžete aplikaci dočasně nastavit tak, aby používala úplný vztah důvěryhodnosti.</span><span class="sxs-lookup"><span data-stu-id="f7a69-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="f7a69-261">Problém: prostředky "ApplicationPart" jsou externě přístupné</span><span class="sxs-lookup"><span data-stu-id="f7a69-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="f7a69-262">Pokud sestavení obsahuje objekty, které jsou odvozeny z třídy `ApplicationPart`, jsou prostředky tohoto sestavení zpřístupněny třídou `ResourceRouteHandler`.</span><span class="sxs-lookup"><span data-stu-id="f7a69-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="f7a69-263">Podívejte se například na následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="f7a69-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="f7a69-264">Tento požadavek stáhne všechny řetězce prostředků v sestavení *System. Web. webpages. Administration. dll* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="f7a69-265">Stáhnou se všechny integrované prostředky (dokonce i ty, které nejsou určené k obsluhování jako statický obsah).</span><span class="sxs-lookup"><span data-stu-id="f7a69-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="f7a69-266">Pokud vložené prostředky obsahují citlivé informace, může to představovat bezpečnostní riziko.</span><span class="sxs-lookup"><span data-stu-id="f7a69-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="f7a69-267">**Alternativní řešení** </span><span class="sxs-lookup"><span data-stu-id="f7a69-267">**Workaround** </span></span>  
> <span data-ttu-id="f7a69-268">Pokud vytvoříte objekt **ApplicationPart** , ujistěte se, že vložené prostředky přidružené k danému sestavení **ApplicationPart** objektu neobsahují citlivé informace.</span><span class="sxs-lookup"><span data-stu-id="f7a69-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="f7a69-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="f7a69-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="f7a69-270">Informace o problémech s instalací pro WebMatrix najdete v části [potíže s instalací WebMatrix](#Known_Issues_Installation) výše v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

<span data-ttu-id="f7a69-271">Tato část dokumentu popisuje známé problémy pro vývojové prostředí WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="f7a69-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="f7a69-272">Problém: změny uživatelského jména nebo hesla databázového připojovacího řetězce v souboru Web. config se neprojeví v pracovním prostoru databáze.</span><span class="sxs-lookup"><span data-stu-id="f7a69-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="f7a69-273">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="f7a69-274">V souboru *Web. config* změňte název databáze v připojovacím řetězci (například přidat "1").</span><span class="sxs-lookup"><span data-stu-id="f7a69-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="f7a69-275">Uložte soubor *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="f7a69-276">Klikněte na **databáze** a aktualizujte.</span><span class="sxs-lookup"><span data-stu-id="f7a69-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="f7a69-277">Změňte název databáze v připojovacím řetězci v souboru *Web. config* zpět na původní název databáze.</span><span class="sxs-lookup"><span data-stu-id="f7a69-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="f7a69-278">Uložte soubor *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="f7a69-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="f7a69-279">Klikněte na **databáze** a aktualizujte.</span><span class="sxs-lookup"><span data-stu-id="f7a69-279">Click **Databases** and refresh.</span></span>

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="f7a69-280">Problém: složky vytvořené pomocí WebMatrixu se nedají odstranit.</span><span class="sxs-lookup"><span data-stu-id="f7a69-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="f7a69-281">Pokud je WebMatrix spuštěný pomocí zvýšených oprávnění (to znamená, že jste spustili WebMatrix pomocí možnosti **Spustit jako správce** ve Windows), složky, které jsou vytvořené pomocí WebMatrixu, se nedají odstranit pomocí Průzkumníka Windows.</span><span class="sxs-lookup"><span data-stu-id="f7a69-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="f7a69-282">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-282">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-283">Spusťte Průzkumníka Windows pomocí zvýšených oprávnění.</span><span class="sxs-lookup"><span data-stu-id="f7a69-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="f7a69-284">Postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="f7a69-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="f7a69-285">V systému Windows klikněte na tlačítko **Start**.</span><span class="sxs-lookup"><span data-stu-id="f7a69-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="f7a69-286">Zadejte "Průzkumník Windows" a klikněte pravým tlačítkem myši na položku **Průzkumník Windows**.</span><span class="sxs-lookup"><span data-stu-id="f7a69-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="f7a69-287">Klikněte na **Spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="f7a69-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="f7a69-288">Pak můžete složky odstranit.</span><span class="sxs-lookup"><span data-stu-id="f7a69-288">You can then delete the folders.</span></span>

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="f7a69-289">Problém: WebMatrix 1,0 není schopen provádět určité úlohy, které vyžadují zvýšení úrovně oprávnění.</span><span class="sxs-lookup"><span data-stu-id="f7a69-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="f7a69-290">WebMatrix 1,0 není schopen provádět určité úlohy, které vyžadují zvýšení oprávnění, jako je například instalace dalších součástí v následujících situacích:</span><span class="sxs-lookup"><span data-stu-id="f7a69-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="f7a69-291">V systému Windows Vista nebo Windows 7 jste přihlášeni pomocí účtu, který nemá oprávnění správce a nástroj řízení uživatelských účtů (UAC) je zakázán.</span><span class="sxs-lookup"><span data-stu-id="f7a69-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="f7a69-292">Používáte Microsoft Windows XP nebo Microsoft Windows Server 2003.</span><span class="sxs-lookup"><span data-stu-id="f7a69-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="f7a69-293">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-293">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-294">Většina úloh v WebMatrixu 1,0 nevyžaduje oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="f7a69-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="f7a69-295">V případě, že to uděláte, můžete tuto operaci provést jako správce nebo postupovat podle následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="f7a69-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="f7a69-296">V systému Windows Vista nebo Windows 7 povolte nástroj řízení uživatelských účtů.</span><span class="sxs-lookup"><span data-stu-id="f7a69-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="f7a69-297">V systému Windows XP přidejte uživatele do skupiny zabezpečení Správci.</span><span class="sxs-lookup"><span data-stu-id="f7a69-297">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="f7a69-298">Problém: lokalita z webové galerie je zakázaná.</span><span class="sxs-lookup"><span data-stu-id="f7a69-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="f7a69-299">Možnost **web z Galerie webu** je zakázána, pokud není nainstalována instalace webové platformy 3,0.</span><span class="sxs-lookup"><span data-stu-id="f7a69-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="f7a69-300">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-300">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-301">Nainstalujte [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="f7a69-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="f7a69-302">Problém: Google Chrome není k dispozici jako možnost spuštění.</span><span class="sxs-lookup"><span data-stu-id="f7a69-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="f7a69-303">Google Chrome se v seznamu **Spustit** na kartě **Domů** nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="f7a69-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="f7a69-304">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-304">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-305">Některé verze Google Chrome se neregistrují správně s funkcí výchozí programy v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="f7a69-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="f7a69-306">Jako alternativní řešení spusťte Google Chrome, klikněte na nabídku *přizpůsobit a řídit Google Chrome* , klikněte na *Možnosti*a potom klikněte na *nastavit Google Chrome výchozí prohlížeč*.</span><span class="sxs-lookup"><span data-stu-id="f7a69-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="f7a69-307">Problém: dialogové okno cizí klíč nepovoluje zadávání primárního klíče.</span><span class="sxs-lookup"><span data-stu-id="f7a69-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="f7a69-308">Dialogové okno **cizí klíč** vám neumožňuje zadat název primárního klíče z tabulky primárního klíče.</span><span class="sxs-lookup"><span data-stu-id="f7a69-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="f7a69-309">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-309">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-310">To je úmyslné.</span><span class="sxs-lookup"><span data-stu-id="f7a69-310">This is intentional.</span></span> <span data-ttu-id="f7a69-311">Nemusíte zadávat název primárního klíče z tabulky primárního klíče.</span><span class="sxs-lookup"><span data-stu-id="f7a69-311">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="f7a69-312">Problém: IntelliSense není k dispozici ve WebMatrixu pro C#syntaxe Razor, nebo Visual Basic</span><span class="sxs-lookup"><span data-stu-id="f7a69-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="f7a69-313">Technologie IntelliSense je podporována v WebMatrixu pro HTML a CSS.</span><span class="sxs-lookup"><span data-stu-id="f7a69-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="f7a69-314">Není ale k dispozici pro jiné jazyky.</span><span class="sxs-lookup"><span data-stu-id="f7a69-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="f7a69-315">**Alternativní řešení** </span><span class="sxs-lookup"><span data-stu-id="f7a69-315">**Workaround** </span></span>  
> <span data-ttu-id="f7a69-316">Žádné.</span><span class="sxs-lookup"><span data-stu-id="f7a69-316">None.</span></span>

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="f7a69-317">Problém: technologie IntelliSense pro HTML a CSS navrhuje prvky, které nejsou kontextově vhodné</span><span class="sxs-lookup"><span data-stu-id="f7a69-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="f7a69-318">Technologie IntelliSense pro značky ve WebMatrixu podporuje HTML pomocí [přechodného schématu XHTML 1,0](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) a šablon stylů CSS pomocí [schématu CSS 2,1](http://www.w3.org/TR/CSS2/).</span><span class="sxs-lookup"><span data-stu-id="f7a69-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="f7a69-319">Vzhledem k tomu, že je technologie IntelliSense založena na těchto specifických schématech, mohou být doporučeny určité značky, atributy nebo vlastnosti, které nejsou vhodné pro aktuální definici stránky nebo stylu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="f7a69-320">V případě HTML může také vést k neočekávaným návrhům v obsahu, který může být interpretován jako nesprávně vytvořený kód XHTML (například když nejsou značky uzavřeny).</span><span class="sxs-lookup"><span data-stu-id="f7a69-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="f7a69-321">Tento problém může být více patrné, pokud je kurzor uvnitř nekompletní značky; v takovém případě může IntelliSense navrhovat nové úvodní značky nebo nabízet jiné nesprávné návrhy.</span><span class="sxs-lookup"><span data-stu-id="f7a69-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="f7a69-322">**Alternativní řešení** </span><span class="sxs-lookup"><span data-stu-id="f7a69-322">**Workaround** </span></span>  
> <span data-ttu-id="f7a69-323">V případě jazyka HTML se ujistěte, že pracujete v rámci dobře formátované a kompletní stránky XHTML.</span><span class="sxs-lookup"><span data-stu-id="f7a69-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="f7a69-324">Pro šablony stylů CSS neexistuje žádné alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="f7a69-324">For CSS, there is no workaround.</span></span>

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="f7a69-325">Problém: při psaní není vyvolána technologie IntelliSense</span><span class="sxs-lookup"><span data-stu-id="f7a69-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="f7a69-326">V důsledku toho nemusí být technologie IntelliSense vyvolána, protože v editoru je zadán kód HTML nebo šablona stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="f7a69-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="f7a69-327">Konkrétně k tomu může dojít, když je kurzor přímo vedle jiného prvku nebo na konci souboru.</span><span class="sxs-lookup"><span data-stu-id="f7a69-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="f7a69-328">**Alternativní řešení** </span><span class="sxs-lookup"><span data-stu-id="f7a69-328">**Workaround** </span></span>  
> <span data-ttu-id="f7a69-329">Zajistěte, aby kolem místa vložení bylo prázdné místo, a že kurzor není na konci souboru.</span><span class="sxs-lookup"><span data-stu-id="f7a69-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="f7a69-330">IntelliSense můžete také vyvolat ručně stisknutím kombinace kláves CTRL + MEZERNÍK.</span><span class="sxs-lookup"><span data-stu-id="f7a69-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="f7a69-331">Problém: pro zakázání IntelliSense není k dispozici žádné uživatelské rozhraní.</span><span class="sxs-lookup"><span data-stu-id="f7a69-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="f7a69-332">WebMatrix 1,0 neposkytuje žádné uživatelské rozhraní ani gesto pro zakázání technologie IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="f7a69-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="f7a69-333">**Alternativní řešení** </span><span class="sxs-lookup"><span data-stu-id="f7a69-333">**Workaround** </span></span>  
> <span data-ttu-id="f7a69-334">Spusťte WebMatrix pomocí následujícího příkazu, který obsahuje přepínač zakazující technologii IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="f7a69-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="f7a69-335">IIS Express</span><span class="sxs-lookup"><span data-stu-id="f7a69-335">IIS Express</span></span>

<span data-ttu-id="f7a69-336">IIS Express má vlastní soubor Readme, který je k dispozici na následující adrese URL:</span><span class="sxs-lookup"><span data-stu-id="f7a69-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="f7a69-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x405</span><span class="sxs-lookup"><span data-stu-id="f7a69-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="f7a69-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="f7a69-338">SQL Server Compact</span></span>

<span data-ttu-id="f7a69-339">SQL Server Compact má vlastní soubor Readme, který je k dispozici na následující adrese URL:</span><span class="sxs-lookup"><span data-stu-id="f7a69-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="f7a69-340">Informace o problémech, které zahrnují instalaci SQL Server Compact jako součást webové matrice, najdete v části [potíže při instalaci WebMatrix](#Known_Issues_Installation) výše v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a><span data-ttu-id="f7a69-341">Instalace aplikací</span><span class="sxs-lookup"><span data-stu-id="f7a69-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="f7a69-342">Problém: instalace aplikace může trvat dlouhou dobu, pokud se složka Dokumenty uživatele přesměruje na sdílenou síťovou složku.</span><span class="sxs-lookup"><span data-stu-id="f7a69-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="f7a69-343">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-343">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-344">Žádné.</span><span class="sxs-lookup"><span data-stu-id="f7a69-344">None.</span></span> <span data-ttu-id="f7a69-345">Instalace aplikace může nějakou dobu trvat, ale nainstaluje se správně.</span><span class="sxs-lookup"><span data-stu-id="f7a69-345">The application might take a while to install, but will install correctly.</span></span>

### <a id="Known_Issues_Publishing_Applications"></a><span data-ttu-id="f7a69-346">Publikování aplikací</span><span class="sxs-lookup"><span data-stu-id="f7a69-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="f7a69-347">Problém: při publikování SQL Compact Database nejde získat povinná oprávnění.</span><span class="sxs-lookup"><span data-stu-id="f7a69-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="f7a69-348">WebMatrix plně nepodporuje nasazení podpůrných binárních souborů pro SQL Server Compact na server, na kterém běží .NET Framework verze 3,5 s konfigurací středně důvěryhodného vztahu důvěryhodnosti.</span><span class="sxs-lookup"><span data-stu-id="f7a69-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="f7a69-349">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-349">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-350">Upřednostňovaným řešením je instalace .NET Framework 4 na server.</span><span class="sxs-lookup"><span data-stu-id="f7a69-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="f7a69-351">Případně proveďte následující:</span><span class="sxs-lookup"><span data-stu-id="f7a69-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="f7a69-352">Do části `SecurityClasses` v souboru *Web\_MediumTrust. config* přidejte následující prvky:</span><span class="sxs-lookup"><span data-stu-id="f7a69-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="f7a69-353">Vytvořte novou sadu oprávnění v souboru *Web\_MediumTrust. config* s následujícími požadovanými oprávněními:</span><span class="sxs-lookup"><span data-stu-id="f7a69-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="f7a69-354">Použijte sadu oprávnění na SQL Server Compact tím, že do souboru *Web\_MediumTrust. config* vložíte následující prvky:</span><span class="sxs-lookup"><span data-stu-id="f7a69-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="f7a69-355">Problém: galerie a webové aplikace PhpBB po publikování zobrazují chybu služba není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="f7a69-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="f7a69-356">V některých případech publikování aplikace způsobí chybu "služba není k dispozici".</span><span class="sxs-lookup"><span data-stu-id="f7a69-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="f7a69-357">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-357">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-358">Ve WebMatrixu přidejte zpětné lomítko (\) na konec názvu serveru v okně **Nastavení publikování** a pak aplikaci znovu publikujte.</span><span class="sxs-lookup"><span data-stu-id="f7a69-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="f7a69-359">Problém: rozložení webu Moodle a odkazy se po publikování přeruší.</span><span class="sxs-lookup"><span data-stu-id="f7a69-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="f7a69-360">Po publikování aplikace Moodle aplikace nefunguje správně.</span><span class="sxs-lookup"><span data-stu-id="f7a69-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="f7a69-361">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-361">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-362">Ve WebMatrixu přidejte lomítko (/) na konec pole **název webu** v okně **Nastavení publikování** a pak znovu publikujte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f7a69-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="f7a69-363">Problém: publikování nopCommerce se nezdařilo s chybou databáze</span><span class="sxs-lookup"><span data-stu-id="f7a69-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="f7a69-364">Publikování nopCommerce se nepovede a ohlásí chybu v databázi, jako je "vložení do tabulky protokolu NOP\_se nezdařilo."</span><span class="sxs-lookup"><span data-stu-id="f7a69-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="f7a69-365">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="f7a69-366">V nabídce WebMatrix klikněte na **Spustit** , aby se NopCommerce spouštěla místně.</span><span class="sxs-lookup"><span data-stu-id="f7a69-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="f7a69-367">Přihlaste se na stránku Správa.</span><span class="sxs-lookup"><span data-stu-id="f7a69-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="f7a69-368">Klikněte na nabídku **systém** .</span><span class="sxs-lookup"><span data-stu-id="f7a69-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="f7a69-369">Klikněte na možnost **protokol** .</span><span class="sxs-lookup"><span data-stu-id="f7a69-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="f7a69-370">Klikněte na tlačítko **Vymazat protokol**.</span><span class="sxs-lookup"><span data-stu-id="f7a69-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="f7a69-371">Publikujte nopCommerce znovu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-371">Publish nopCommerce again.</span></span>

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="f7a69-372">Problém: SilverStripe CMS zobrazí při stažení publikované lokality chybu FCGI PHP protokolu HTTP 500.</span><span class="sxs-lookup"><span data-stu-id="f7a69-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="f7a69-373">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-373">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-374">Po kliknutí na **Stáhnout publikovaný web**vynechejte `silverstripe-cache/manifest_main` v **publikování Preview**.</span><span class="sxs-lookup"><span data-stu-id="f7a69-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="f7a69-375">Tento soubor se používá pro účely ukládání do mezipaměti a je specifický pro každý počítač.</span><span class="sxs-lookup"><span data-stu-id="f7a69-375">This file is used for caching purposes and is specific to each computer.</span></span>

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="f7a69-376">Problém: při stahování publikované lokality se u podtextu zobrazí zpráva "Chyba serveru v aplikaci/".</span><span class="sxs-lookup"><span data-stu-id="f7a69-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="f7a69-377">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-377">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-378">Otevřete soubor *Web. config* webu a v připojovacím řetězci databáze nahraďte ID a heslo uživatele pomocí přihlašovacích údajů správce SQL Server (přihlašovací údaje SA).</span><span class="sxs-lookup"><span data-stu-id="f7a69-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="f7a69-379">Případně můžete pomocí těchto kroků udělit uživatelskému účtu, ke kterému jste přihlášeni, oprávnění `db_owner`:</span><span class="sxs-lookup"><span data-stu-id="f7a69-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="f7a69-380">Nainstalujte SQL Server Management Studio pomocí instalačního programu webové platformy.</span><span class="sxs-lookup"><span data-stu-id="f7a69-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="f7a69-381">Připojte se k místní instanci SQL Server Express (ve výchozím nastavení `.\SQLEXPRESS`).</span><span class="sxs-lookup"><span data-stu-id="f7a69-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="f7a69-382">Klikněte na **databáze** &gt; *[LocalSubtextDatabase]* &gt; **zabezpečení** &gt; **uživatele** &gt; *[localSubtextUser*] (výchozí nastavení je `subtextuser`], klikněte pravým tlačítkem myši a klikněte na **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="f7a69-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="f7a69-383">V části členství v roli vyberte **db\_vlastník** .</span><span class="sxs-lookup"><span data-stu-id="f7a69-383">Select **db\_owner** in the role membership section.</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="f7a69-384">Problém: po publikování nemusí lokalita fungovat, pokud se v poli Cílová adresa URL nepoužívá předpona http://nebo https://.</span><span class="sxs-lookup"><span data-stu-id="f7a69-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="f7a69-385">Pokud v dialogovém okně **Nastavení publikování** nezačíná cílová adresa URL `http://` nebo `https://`, web po nasazení nemusí fungovat.</span><span class="sxs-lookup"><span data-stu-id="f7a69-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="f7a69-386">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-386">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-387">Ujistěte se, že před publikováním webu se v dialogovém okně **Nastavení publikování** spustí cílová adresa URL s `http://` nebo `https://`.</span><span class="sxs-lookup"><span data-stu-id="f7a69-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="f7a69-388">Problém: publikování databáze MySQL se nepovede kvůli chybě: publikování databáze se nepovedlo.</span><span class="sxs-lookup"><span data-stu-id="f7a69-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="f7a69-389">K tomu může dojít, pokud Vzdálená databáze nemůže skript spustit. "</span><span class="sxs-lookup"><span data-stu-id="f7a69-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="f7a69-390">K této chybě může dojít z několika důvodů.</span><span class="sxs-lookup"><span data-stu-id="f7a69-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="f7a69-391">Jedním z důvodů, proč se tato chyba zobrazuje, je, že databázový skript obsahuje znak jednoduché uvozovky (') a výchozí znaková sada databáze MySQL není UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f7a69-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="f7a69-392">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-392">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-393">Nastavte výchozí znakovou sadu pro vzdálenou databázi MySQL na UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f7a69-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="f7a69-394">Problém: některé odkazy nejsou v DotNetNuke viditelné po publikování nebo stahování webu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="f7a69-395">Pokud publikujete nebo stáhnete web DotNetNuke, možná budete muset vymazat mezipaměť a získat tak nové odkazy, které se zobrazí na webu.</span><span class="sxs-lookup"><span data-stu-id="f7a69-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="f7a69-396">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="f7a69-397">Přihlaste se jako hostitel.</span><span class="sxs-lookup"><span data-stu-id="f7a69-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="f7a69-398">Přejděte do nabídky hostitel a vyberte **Nastavení hostitele**.</span><span class="sxs-lookup"><span data-stu-id="f7a69-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="f7a69-399">Přejděte dolů a v části **Upřesnit nastavení**rozbalte položku **Nastavení výkonu**.</span><span class="sxs-lookup"><span data-stu-id="f7a69-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="f7a69-400">Klikněte na odkaz **Vymazat mezipaměť** pro stránky.</span><span class="sxs-lookup"><span data-stu-id="f7a69-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="f7a69-401">Přejít do dolní části stránky a restartovat aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f7a69-401">Go to the bottom of the page and restart the application.</span></span>

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="f7a69-402">Problém: některé odkazy v AtomSite se po stažení publikované lokality poruší.</span><span class="sxs-lookup"><span data-stu-id="f7a69-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="f7a69-403">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-403">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-404">V souboru *Service. config* , *Users. config* a všechny soubory *. XML* nahraďte řetězec adresy URL (například `http://myhost.com/atomsite`) místním souborem (například `http://localhost:1239`).</span><span class="sxs-lookup"><span data-stu-id="f7a69-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="f7a69-405">Problém: aplikace založené na MySQL, jako je WordPress, se nepodařilo publikovat a nahlásit chybu databáze.</span><span class="sxs-lookup"><span data-stu-id="f7a69-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="f7a69-406">Ve výchozím nastavení WebMatrix nainstaluje MySQL se znakovou sadou UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f7a69-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="f7a69-407">Pokud si MySQL nainstalujete sami a znaková sada není UTF-8 (například je Latin1), může proces publikování pro databáze selhat.</span><span class="sxs-lookup"><span data-stu-id="f7a69-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="f7a69-408">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="f7a69-409">Změňte znakovou sadu pro MySQL na UTF-8.</span><span class="sxs-lookup"><span data-stu-id="f7a69-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="f7a69-410">(Podrobnosti najdete v tématu [znaková sada serveru a kolace](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) na webu MySQL.)</span><span class="sxs-lookup"><span data-stu-id="f7a69-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="f7a69-411">Přeinstalujte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f7a69-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="f7a69-412">Znovu publikujte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f7a69-412">Republish the application.</span></span>

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="f7a69-413">Problém: u aplikací, které mají instalaci prostřednictvím prohlížeče, se nezdařila možnost stáhnout publikovaný web.</span><span class="sxs-lookup"><span data-stu-id="f7a69-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="f7a69-414">Některé aplikace (například Kentico CMS) vyžadují jejich spuštění v prohlížeči, aby bylo možné provést instalaci po instalaci, jako je například vytvoření databáze.</span><span class="sxs-lookup"><span data-stu-id="f7a69-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="f7a69-415">Pokud publikujete aplikaci, například bez dokončení instalace na základě prohlížeče, pokus o stažení stejné lokality ze vzdáleného serveru se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="f7a69-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="f7a69-416">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-416">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-417">Před publikováním webu dokončete instalační program na základě prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="f7a69-417">Finish browser-based setup before publishing the site.</span></span>

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="f7a69-418">Problém: "stažení publikovaného webu" se nezdařila s chybou databáze pro DotNetNuke a Kooboo CMS</span><span class="sxs-lookup"><span data-stu-id="f7a69-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="f7a69-419">Pokud se pokusíte stáhnout aplikaci ze serveru a máte přihlašovací údaje správce v připojovacím řetězci databáze v dialogovém okně **publikování nastavení** , může se v protokolu publikování zobrazit následující chyba:</span><span class="sxs-lookup"><span data-stu-id="f7a69-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="f7a69-420">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="f7a69-420">**Workaround**</span></span>  
> <span data-ttu-id="f7a69-421">Pokud je to praktické, publikujte lokalitu (nebo ji publikujte) pomocí přihlašovacích údajů bez oprávnění správce pro databázi.</span><span class="sxs-lookup"><span data-stu-id="f7a69-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="f7a69-422">Další informace</span><span class="sxs-lookup"><span data-stu-id="f7a69-422">For More Information</span></span>

<span data-ttu-id="f7a69-423">Další informace o WebMatrixu 1,0 najdete na následujících webech:</span><span class="sxs-lookup"><span data-stu-id="f7a69-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="f7a69-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="f7a69-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="f7a69-425">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f7a69-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="f7a69-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="f7a69-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="f7a69-427">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="f7a69-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="f7a69-428">Všechna práva vyhrazena.</span><span class="sxs-lookup"><span data-stu-id="f7a69-428">All Rights Reserved.</span></span> <span data-ttu-id="f7a69-429">[Podmínek použití](https://msdn.microsoft.cos/cc300389.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7a69-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
