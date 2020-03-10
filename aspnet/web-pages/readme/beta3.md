---
uid: web-pages/readme/beta3
title: Readme (Web Matrix) a ASP.NET Web Pages (Razor) beta 3 pro vydání verze | Microsoft Docs
author: rick-anderson
description: Soubor Readme o nástroji WebMatrix a webových stránkách ASP.NET (Razor) verze Beta 3
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628896"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="8c9e2-103">Soubor Readme o nástroji WebMatrix a webových stránkách ASP.NET (Razor) verze Beta 3</span><span class="sxs-lookup"><span data-stu-id="8c9e2-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

> <span data-ttu-id="8c9e2-104">Soubor Readme o nástroji WebMatrix a webových stránkách ASP.NET (Razor) verze Beta 3</span><span class="sxs-lookup"><span data-stu-id="8c9e2-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="8c9e2-105">9\. listopadu 2010</span><span class="sxs-lookup"><span data-stu-id="8c9e2-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="8c9e2-106">Obsah</span><span class="sxs-lookup"><span data-stu-id="8c9e2-106">Contents</span></span>

- [<span data-ttu-id="8c9e2-107">Přehled</span><span class="sxs-lookup"><span data-stu-id="8c9e2-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="8c9e2-108">Instalace</span><span class="sxs-lookup"><span data-stu-id="8c9e2-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="8c9e2-109">Nové funkce, změny a známé problémy ve verzi beta 3</span><span class="sxs-lookup"><span data-stu-id="8c9e2-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="8c9e2-110">Problémy s instalací WebMatrixu</span><span class="sxs-lookup"><span data-stu-id="8c9e2-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="8c9e2-111">Webové stránky ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8c9e2-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="8c9e2-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="8c9e2-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="8c9e2-113">Instalace aplikací</span><span class="sxs-lookup"><span data-stu-id="8c9e2-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="8c9e2-114">Publikování aplikací</span><span class="sxs-lookup"><span data-stu-id="8c9e2-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="8c9e2-115">Další problémy</span><span class="sxs-lookup"><span data-stu-id="8c9e2-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="8c9e2-116">Další informace</span><span class="sxs-lookup"><span data-stu-id="8c9e2-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="8c9e2-117">Přehled</span><span class="sxs-lookup"><span data-stu-id="8c9e2-117">Overview</span></span>

> <span data-ttu-id="8c9e2-118">Microsoft WebMatrix beta je bezplatný sada pro vývoj na webu, která se instaluje během několika minut.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="8c9e2-119">Integruje webový server s databázovými a programovacími rozhraními k vytvoření jediného integrovaného prostředí.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="8c9e2-120">Pomocí WebMatrixu beta můžete zjednodušit způsob, jakým kód, otestujete a publikujete vlastní web ASP.NET nebo PHP, nebo můžete pomocí WebMatrixu beta začít nový web pomocí oblíbených open source aplikací, jako je DotNetNuke, Umbraco, WordPress nebo Joomla.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="8c9e2-121">WebMatrix beta používá stejné výkonné prostředí webového serveru, databázového stroje a rozhraní, které spustí vaši webovou stránku na internetu, což usnadňuje přechod od vývoje k produkčnímu a bezproblémovému fungování.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="8c9e2-122">Instalace</span><span class="sxs-lookup"><span data-stu-id="8c9e2-122">Installation</span></span>

> <span data-ttu-id="8c9e2-123">K instalaci WebMatrixu beta 3 použijete [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="8c9e2-124">Po instalaci instalačního programu webové platformy ho můžete použít k instalaci WebMatrixu beta 3.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="8c9e2-125">Pokud máte při instalaci problémy, přečtěte si téma [řešení potíží s instalace webové platformy Microsoft](https://go.microsoft.com/fwlink/?LinkId=196212).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="8c9e2-126">Pokyny k publikování aplikací</span><span class="sxs-lookup"><span data-stu-id="8c9e2-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="8c9e2-127">Přečtěte si podrobné [pokyny pro publikování aplikací](https://go.microsoft.com/fwlink/?LinkID=196149) .</span><span class="sxs-lookup"><span data-stu-id="8c9e2-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="8c9e2-128">Nové funkce, změny, problémy s andKnown</span><span class="sxs-lookup"><span data-stu-id="8c9e2-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="8c9e2-129">Instalace WebMatrix beta 3</span><span class="sxs-lookup"><span data-stu-id="8c9e2-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="8c9e2-130">Problém: WebMatrix beta 3 je dostupný jenom na platformách, které podporují Microsoft .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="8c9e2-131">Pro WebMatrix beta se vyžaduje .NET Framework verze 4.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="8c9e2-132">V některých případech se instalační program WebMatrix beta pokusí nainstalovat na platformu, která není součástí podporované konfigurační sady.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="8c9e2-133">Konkrétně Windows Vista bez aktualizace SP1 vám umožní zahájit instalaci WebMatrixu beta, ale komponenta .NET Framework 4 selže a zablokuje instalaci.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="8c9e2-134">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-134">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-135">Nainstalujte na podporovanou platformu, která zahrnuje:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="8c9e2-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8c9e2-136">Windows 7</span></span>
> - <span data-ttu-id="8c9e2-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="8c9e2-137">Windows Server 2008</span></span>
> - <span data-ttu-id="8c9e2-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="8c9e2-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="8c9e2-139">Windows Vista SP1 nebo novější</span><span class="sxs-lookup"><span data-stu-id="8c9e2-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="8c9e2-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="8c9e2-140">Windows XP SP3</span></span>
> - <span data-ttu-id="8c9e2-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="8c9e2-141">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="8c9e2-142">Problém: nejde nainstalovat WebMatrix beta 3, pokud je nainstalovaná Microsoft Visual Studio 2008 bez Microsoft Visual Studio 2008 SP1.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="8c9e2-143">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-143">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-144">Nainstalujte [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) z webu Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="8c9e2-145">Problém: některá sestavení pro SQL Server Compact 4,0 nejsou v globální mezipaměti sestavení (GAC) nainstalovaná.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="8c9e2-146">Spravovaná sestavení pro SQL Server Compact 4,0 nejsou vložena do globální mezipaměti sestavení (GAC) při instalaci SQL Server Compact 4,0 na počítači 64 a počítač má nainstalovaný pouze klientský profil .NET Framework 3,5 SP1.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="8c9e2-147">Spravovaná sestavení, která nejsou nainstalovaná v globální mezipaměti sestavení (GAC), jsou:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="8c9e2-148">*System. data. SqlServerCe. dll* (poskytovatel ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="8c9e2-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="8c9e2-149">*System. data. SqlServerCe. entity. dll* (ADO.NET Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="8c9e2-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="8c9e2-150">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-150">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-151">Odinstalujte SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="8c9e2-152">Úplnou verzi .NET Framework 3,5 SP1 si stáhněte a nainstalujte z následujícího umístění:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="8c9e2-153">Microsoft .NET Framework 3,5 Service Pack 1 (úplný balíček)</span><span class="sxs-lookup"><span data-stu-id="8c9e2-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="8c9e2-154">Pak přeinstalujte SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-154">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="8c9e2-155">Problém: SQL Server Compact nejde odinstalovat pomocí příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="8c9e2-156">Odinstalace SQL Server Compact pomocí možností příkazového řádku nefunguje v této verzi.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="8c9e2-157">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-157">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-158">Pomocí *programů a funkcí* v Ovládacích panelech systému Windows odinstalujte Microsoft SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="8c9e2-159">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="8c9e2-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="8c9e2-160">Tato část dokumentu popisuje nové funkce, změny a známé problémy ve verzi beta 3 webových stránek ASP.NET s syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="8c9e2-161">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="8c9e2-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="8c9e2-162">Provedeny</span><span class="sxs-lookup"><span data-stu-id="8c9e2-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="8c9e2-163">Problémy</span><span class="sxs-lookup"><span data-stu-id="8c9e2-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="8c9e2-164">Nové funkce ve verzi beta 3 pro webové stránky ASP.NET se syntaxí Razor</span><span class="sxs-lookup"><span data-stu-id="8c9e2-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="8c9e2-165">Novinka: metoda "HTML. Raw" vykresluje nekódovaný kód</span><span class="sxs-lookup"><span data-stu-id="8c9e2-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="8c9e2-166">Nová metoda `Html.Raw` umožňuje vykreslení značky HTML jako značky namísto vykreslování kódovaného výstupu.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="8c9e2-167">(Ve výchozím nastavení ASP.NET Razor kóduje řetězce před jejich vykreslením.) Syntaxe je:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="8c9e2-168">Následující příklad ukazuje, jak použít `Html.Raw`:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="8c9e2-169">Změny ve verzi beta 3 pro webové stránky ASP.NET se syntaxí Razor</span><span class="sxs-lookup"><span data-stu-id="8c9e2-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="8c9e2-170">Změna: metoda "HrefAttribute" byla odebrána.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="8c9e2-171">Metoda `HrefAttribute` třídy `WebPage` byla odebrána.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="8c9e2-172">Tato pomoc se použila ke kódování nebezpečných znaků v adresách URL.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="8c9e2-173">Již není vyžadován, protože ASP.NET Razor automaticky kóduje řetězce.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="8c9e2-174">(K vykreslování nekódovaných řetězců použijte novou metodu `Html.Raw`.)</span><span class="sxs-lookup"><span data-stu-id="8c9e2-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="8c9e2-175">Změna: syntaxe deklarativních pomocníků "@helper" se změnila</span><span class="sxs-lookup"><span data-stu-id="8c9e2-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="8c9e2-176">Ve verzi beta 3 ASP.NET mění způsob, jakým analyzuje pomocníky vytvořené pomocí syntaxe `@helper`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="8c9e2-177">V podstatě se syntaxe `@helper` nyní analyzuje jako blok kódu namísto jako blok značek, které mohou obsahovat kód.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="8c9e2-178">Proto kód uvnitř pomocné rutiny nemusí být uzavřen do `@{ }`ch bloků.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="8c9e2-179">V opačném případě se značky uvnitř pomocné rutiny musí explicitně zahrnout do prvků HTML nebo do značek ASP.NET Razor `<text></text>`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="8c9e2-180">Například následující syntaxe `@helper` funguje ve verzi beta 3:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="8c9e2-181">Ve verzi beta 3 se tato pomocná Nápověda musí změnit tak, aby vypadala jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="8c9e2-182">Všimněte si, že `@{ }` znaky kolem počátečního kódu v pomocné rutině již nejsou používány.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="8c9e2-183">Důvodem je to, že obsah pomocníků je ve výchozím nastavení považován za blok kódu.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="8c9e2-184">Pomocné rutiny vykresluje kód, který začíná otevírací `<a>`ovou značkou.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="8c9e2-185">Pokud musí pomoc vykreslovat prostý text nebo značky, které neobsahují uzavírací značku (například `<meta>` značky), musí být obsah, který se má vykreslit, v `<text></text>` značek.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>

#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="8c9e2-186">Změna: WebPageContext. HttpContext se odstranilo.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="8c9e2-187">Vlastnost `WebPageContext.HttpContext` byla odebrána.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="8c9e2-188">Místo toho použijte `HttpContext.Current`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="8c9e2-189">(Vlastnost `WebPageContext.HttpContext` jednoduše zabalené.)</span><span class="sxs-lookup"><span data-stu-id="8c9e2-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>

#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="8c9e2-190">Změna: Pomocník pro Facebook se přesunul do nového balíčku.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="8c9e2-191">Pomocná rutina `Facebook` byla přesunuta do knihovny *Facebook. Helper* , která obsahuje nápovědu `Facebook` a další funkce.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="8c9e2-192">Tuto knihovnu musíte nainstalovat jako samostatný balíček, jak je popsáno v tématu "instalace pomocníků se správcem balíčků" v kurzu [Začínáme se stránkami ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202889).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="8c9e2-193">Změna: typy členství, rolí a zabezpečení se přesunou do nového sestavení.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="8c9e2-194">Následující typy byly přesunuty do sestavení `WebMatrix.WebData`:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="8c9e2-195">Change: třída "TagBuilder" přesunutá na sestavení System. Web. webpages. dll</span><span class="sxs-lookup"><span data-stu-id="8c9e2-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="8c9e2-196">Třída `TagBuilde` r byla přesunuta do sestavení System. Web. webpages. dll.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="8c9e2-197">Dřív to bylo v sestavení, které bylo součástí ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="8c9e2-198">Tato změna znamená, že nemusíte instalovat ASP.NET MVC, aby bylo možné použít třídu `TagBuilder`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="8c9e2-199">Nicméně třída je stále v oboru názvů `System.Web.Mvc`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="8c9e2-200">Aby bylo možné použít třídu `TagBuilder` (například ve vlastním Pomocníkovi ASP.NET Razor), musíte odkazovat na obor názvů (například přidáním `@using System.Web.Mvc` do kódu).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="8c9e2-201">Změna: syntaxe ověření žádosti se změnila; Odstranila se třída "ověření".</span><span class="sxs-lookup"><span data-stu-id="8c9e2-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="8c9e2-202">Chcete-li zakázat ověřování pro jednotlivá pole nebo sadu polí ve verzi beta 3, můžete zavolat metodu `Validation.Exclude` a předat název nebo názvy polí, které mají být vyloučeny z ověřování.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="8c9e2-203">V rámci verze beta 3 je k dispozici nová syntaxe pro obejít ověření.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="8c9e2-204">Byla odstraněna metoda `Validation` použitá v beta verzi 3.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="8c9e2-205">Pokud nezakážete ověření žádosti, pokud se uživatelé pokusí odeslat kód HTML (například pomocí editoru formátovaného textu na stránce), bude webová stránka hlásit chybu, jako *je potenciálně nebezpečná žádost. z klienta byla zjištěna hodnota formuláře* a vstup uživatele není přijat.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="8c9e2-206">Pokud zakážete ověření žádosti, musíte ručně zkontrolovat vstup uživatele, abyste se ujistili, že neobsahují potenciálně nebezpečné značky nebo skripty, a to jako v případě [knihovny Microsoft Anti-průřezing Scripting Library v 4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="8c9e2-207">Chcete-li zakázat automatické ověřování žádostí, zavolejte metodu `Request.Unvalidated`, předejte jí název pole nebo jiný objekt post, pro který chcete obejít ověření žádosti.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="8c9e2-208">Tuto metodu můžete použít k obejít ověřování pro jakékoli položky v `Form`, `QueryString`, `Cookies`a `ServerVariables` kolekcích.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="8c9e2-209">Následující příklady ukazují, jak používat metodu `Unvalidated`:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="8c9e2-210">Známé problémy pro webové stránky ASP.NET se syntaxí Razor</span><span class="sxs-lookup"><span data-stu-id="8c9e2-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="8c9e2-211">Problém: neočekávané chování při použití vlastní uživatelské tabulky pro členství</span><span class="sxs-lookup"><span data-stu-id="8c9e2-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="8c9e2-212">Chcete-li inicializovat poskytovatele členství pro web ASP.NET Razor, zavoláte metodu `WebSecurity.InitializeDatabaseConnection`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="8c9e2-213">(Ve webové matici úvodní šablona webu obsahuje volání této metody v souboru *\_AppStart. cshtml* .) Pokud je parametr `autoCreateTables` této metody nastaven na hodnotu true (ve výchozím nastavení je nastaven na hodnotu true v šabloně počátečního webu) a pokud je do metody (druhý parametr) předána nerozpoznaný název tabulky, metoda nevyvolá chybu.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="8c9e2-214">Místo toho se tabulka automaticky vytvoří.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="8c9e2-215">To může být problém, pokud máte v úmyslu použít pro členství vlastní uživatelskou tabulku, ale předat do metody `WebSecurity.InitializeDatabaseConnection` špatný název tabulky.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="8c9e2-216">Vzhledem k tomu, že metoda není ve výchozím nastavení vyvolána, pokud zadaná tabulka neexistuje a protože místo toho vytvoří novou tabulku, aplikace může vypadat, že bude fungovat.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="8c9e2-217">Nicméně kód aplikace, který závisí na vlastní uživatelské tabulce (a u polí v ní), může nakonec selhat s neočekávanými chybami.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="8c9e2-218">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-218">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-219">Ujistěte se, že název předaný v metodě `InitializeDatabaseConnection` odpovídá tabulce profilů uživatele v databázi členství, nebo se ujistěte, že parametr `autoCreateTables` je nastaven na hodnotu false.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="8c9e2-220">Problém: nepovedlo se vygenerovat uživatelskou instanci SQL Server, chyba.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="8c9e2-221">Pokud webová aplikace WebMatrix používá SQL Server Express a je v systému Windows 7 nebo Windows Server 2008 R2 spuštěna služba IIS 7,5, může se zobrazit chyba, která indikuje, že SQL Server během běhu nemůže načíst cestu k místní aplikaci uživatele.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="8c9e2-222">**Alternativní řešení** Ujistěte se, že účet systému Windows, pod kterým je aplikace spuštěna (obvykle síťová služba), má oprávnění ke čtení a zápisu pro kořenové složky aplikace a pro podsložky, jako jsou například *data aplikace\_* .</span><span class="sxs-lookup"><span data-stu-id="8c9e2-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="8c9e2-223">Podrobnější informace jsou k dispozici v článku znalostní báze [problémy s SQL Server Expressmi vytvářením uživatelských instancí a projektů webových aplikací ASP.NET](https://support.microsoft.com/kb/2002980).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="8c9e2-224">Problém: v aplikaci Visual Studio se obory názvů pro vlastní sestavení (DLL) neimportují automaticky</span><span class="sxs-lookup"><span data-stu-id="8c9e2-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="8c9e2-225">Použijete-li vlastní sestavení v projektu v aplikaci Visual Studio, obory názvů deklarované v těchto sestaveních nejsou automaticky importovány v době návrhu.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="8c9e2-226">V důsledku toho se odkazy na vlastní typy nemusí rozpoznat v době návrhu a jsou označeny jako nerozpoznané v sadě Visual Studio (pomocí "vlnovek").</span><span class="sxs-lookup"><span data-stu-id="8c9e2-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="8c9e2-227">K tomuto problému dochází pouze v době návrhu v aplikaci Visual Studio; aplikace sama funguje správně.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="8c9e2-228">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-228">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-229">Zahrňte příkaz `using` (`imports` v Visual Basic), který odkazuje na entity, které nejsou v době návrhu rozpoznány.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="8c9e2-230">Problém: Visual Studio IntelliSense a šablony projektů dostupné jenom ve ASP.NET MVC verze 3</span><span class="sxs-lookup"><span data-stu-id="8c9e2-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="8c9e2-231">Při instalaci webových stránek ASP.NET se také neinstalují nástroje pro Visual Studio, jako jsou IntelliSense a šablony projektů pro aplikace ASP.NET Web Pages.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="8c9e2-232">**Alternativní řešení** Chcete-li používat IntelliSense a šablony projektů pro aplikace ASP.NET Web Pages v aplikaci Visual Studio, nainstalujte ASP.NET MVC 3 RC buď prostřednictvím instalačního programu webové platformy, nebo pomocí [samostatného instalačního programu](https://go.microsoft.com/fwlink/?LinkID=191797).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="8c9e2-233">Problém: nepovedlo se najít&gt; třídu&lt;Helper, chyba.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="8c9e2-234">Po upgradu na verzi beta 3 se může zobrazit chyba, že pomocná třída (například třída `Facebook`) nebyla nalezena.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="8c9e2-235">Od verze beta 2 a pokračování ve verzi beta 3 se pomocníki přesunuli na balíčky, které musíte explicitně nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="8c9e2-236">Existující weby nejsou upgradovány, aby zahrnovaly tyto balíčky. To zahrnuje weby ve složkách *\My Documents\IISExpress* nebo *\Dokumenty Documents\My Web Sites* .</span><span class="sxs-lookup"><span data-stu-id="8c9e2-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="8c9e2-237">Konkrétně se zobrazí tato chyba, pokud použijete výchozí web na *stránce moje weby* (WEB1), který obsahuje odkaz na pomocnou nápovědu `Twitter`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="8c9e2-238">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-238">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-239">Zakomentujte volání libovolných pomocníků v lokalitě, spusťte stránku *\_admin* a nainstalujte balíček nebo balíčky, které obsahují pomocníky, které chcete použít.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="8c9e2-240">Po instalaci balíčku můžete odkomentovat řádky, které odkazují na pomocníka.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="8c9e2-241">Problém: nasazení sestavení beta 3 ASP.NET Razor do složky bin nemusí fungovat na hostitelských webech</span><span class="sxs-lookup"><span data-stu-id="8c9e2-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="8c9e2-242">Pokud nasadíte web ASP.NET Web Pages na hostující web a pokud nasadíte sestavení ASP.NET Razor beta 3 do složky *bin* webu, může docházet k chybám, včetně následujících:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="8c9e2-243">K tomu může dojít, pokud poskytovatel hostingu nainstaloval sestavení ASP.NET Web Pages beta 1 do globální mezipaměti aplikace serveru (GAC).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="8c9e2-244">Sestavení v mezipaměti GAC mají přednost před sestaveními nainstalovanými místně ve složce *bin* .</span><span class="sxs-lookup"><span data-stu-id="8c9e2-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="8c9e2-245">**Alternativní řešení** Obraťte se na svého poskytovatele hostingu a ověřte, že chyby, které vidíte, jsou způsobeny konfliktem mezi verzemi sestavení a vaší verze poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="8c9e2-246">Pokud ano, požádejte poskytovatele hostingu, aby aktualizoval sestavení v mezipaměti GAC serveru.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="8c9e2-247">Problém: čtení informačních kanálů nebo jiných externích dat prostřednictvím proxy server</span><span class="sxs-lookup"><span data-stu-id="8c9e2-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="8c9e2-248">Pokud je server, na kterém je spuštěná lokalita, za proxy server, může být nutné nakonfigurovat informace o proxy serveru v souboru *Web. config* , aby bylo možné číst informace, které pocházejí z mimo vaši lokalitu.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="8c9e2-249">Pokud například použijete pomocníka `ReCaptcha`, pomáhající osoba komunikuje se službou reCAPTCHA, ale může být blokována proxy server.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="8c9e2-250">Podobně kanály, které se používají v ASP.NET webové stránky, jako je informační kanál používaný správcem balíčků, můžou vyžadovat konfiguraci proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="8c9e2-251">Pokud dochází k potížím při práci s externí službou nebo při práci s kanálem balíčku, vložte následující prvky do kořenového souboru *Web. config* vaší aplikace:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="8c9e2-252">Další informace o konfiguraci proxy server najdete v tématu [&lt;proxy&gt; elementu (nastavení sítě)](https://msdn.microsoft.com/library/sa91de1e.aspx) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="8c9e2-253">Problém: Chyba "Microsoft. Web. Infrastructure. dll" nelze načíst "</span><span class="sxs-lookup"><span data-stu-id="8c9e2-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="8c9e2-254">Pokud jste dříve nainstalovali verzi beta 1 webových stránek ASP.NET pomocí nástroje syntaxe Razor a potom nainstalujete verzi beta 3, všechna příslušná sestavení jsou nainstalována v globální mezipaměti sestavení (GAC), s výjimkou *Microsoft. Web. Infrastructure. dll*.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="8c9e2-255">V takovém případě se při spuštění ASP.NET Razor Pages zobrazí chyba, která indikuje, že se nepovedlo načíst *Microsoft. Web. Infrastructure. dll* .</span><span class="sxs-lookup"><span data-stu-id="8c9e2-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="8c9e2-256">K tomuto problému dochází, pokud jste načetli verzi beta 3 na čistý počítač.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="8c9e2-257">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-257">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-258">V Ovládacích panelech odinstalujte webové stránky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="8c9e2-259">Pak přeinstalujte verzi beta 3.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-259">Then reinstall the Beta 3 release.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="8c9e2-260">Problém: Odinstalace .NET Framework verze 4: zakáže webové stránky ASP.NET se syntaxí Razor.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="8c9e2-261">Pokud odinstalujete .NET Framework verze 4 a pak ji znovu nainstalujete, ASP.NET webové stránky s syntaxe Razor jsou zakázané.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="8c9e2-262">Stránky s příponou *. cshtml* neběží správně.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="8c9e2-263">Webové stránky ASP.NET registrují sestavení v kořenovém souboru *Web. config* počítače a odebrání .NET Framework Tento soubor odebere.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="8c9e2-264">Opětovná instalace .NET Framework nainstaluje novou verzi konfiguračního souboru, ale nepřidá odkaz pro sestavení webových stránek ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="8c9e2-265">**Alternativní řešení** Po přeinstalaci .NET Framework přeinstalujte webové stránky ASP.NET pomocí syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="8c9e2-266">Tím se do souboru *Web. config* přidá následující element v kořenovém adresáři počítače, který je obvykle v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="8c9e2-267">Problém: aplikace dřív nasazené se ASP.NET sestaveními ve složce Bin se objeví chyby.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="8c9e2-268">Během nasazování kopíruje kopie sestavení webových stránek ASP.NET (například *Microsoft. webpages. dll*) do složky *bin* webu na serveru.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="8c9e2-269">(K této situaci mohlo dojít automaticky během nasazování nebo proto, že vývojář explicitně zkopíroval sestavení.) Pokud je však nainstalována verze beta 3, dojde k chybám, například chybám, které nebyly nalezeny pro určité typy.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="8c9e2-270">K tomu dochází, protože počet typů webových stránek ASP.NET byl přesunut do různých oborů názvů pro verzi beta 3.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="8c9e2-271">**Alternativní řešení** </span><span class="sxs-lookup"><span data-stu-id="8c9e2-271">**Workaround** </span></span>  
> <span data-ttu-id="8c9e2-272">Vymažte složku *bin* nasazené aplikace, zkopírujte nová sestavení do složky (nebo aplikaci znovu nasaďte) a pak aplikaci spusťte znovu.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="8c9e2-273">Problém: adresy URL bez přípony nenaleznou soubory. cshtml/. vbhtml ve službě IIS 7 nebo IIS 7,5</span><span class="sxs-lookup"><span data-stu-id="8c9e2-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="8c9e2-274">V případě služby IIS 7 nebo IIS 7,5 nebudou žádosti s adresou URL, jako jsou následující, schopné najít stránky s příponou *. cshtml* nebo *. vbhtml* :</span><span class="sxs-lookup"><span data-stu-id="8c9e2-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="8c9e2-275">K tomuto problému dochází, protože přepis adres URL není ve výchozím nastavení povolený pro IIS 7 nebo IIS 7,5.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="8c9e2-276">Ve scénáři likeliest se problém nezobrazuje při místním testování pomocí IIS Express, ale při nasazování webu na hostující web dojde k jeho práci.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="8c9e2-277">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="8c9e2-278">Pokud máte kontrolu nad počítačem serveru, na serverovém počítači nainstalujte aktualizaci popsanou v [aktualizaci, která umožňuje určitým obslužným rutinám služby iis 7,0 nebo iis 7,5 zpracovávat požadavky, jejichž adresy URL nekončí tečkou](https://support.microsoft.com/kb/980368).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="8c9e2-279">Pokud nemáte kontrolu nad počítačem serveru (například nasazujete na hostující Web), přidejte následující do souboru *Web. config* webu:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="8c9e2-280">Problém: použití projektu webové aplikace nebo ASP.NET MVC a ASP.NET webových stránek ve stejné aplikaci</span><span class="sxs-lookup"><span data-stu-id="8c9e2-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="8c9e2-281">Pokud jste používali webové stránky v ASP.NET v projektu webové aplikace nebo v aplikaci ASP.NET MVC, může se zobrazit chyba, kterou *WebPageHttpApplication* nelze najít.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="8c9e2-282">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-282">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-283">Pokud se zobrazí tato chyba, změňte základní třídu, ze které je aplikace odvozena.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="8c9e2-284">V souboru *Global. asax* změňte následující řádek:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="8c9e2-285">K tomuto:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="8c9e2-286">To v důsledku toho obrátí změnu, která byla představena pro ASP.NET webové stránky verze beta 1 s syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="8c9e2-287">Problém: nasazení aplikace do počítače, ve kterém není nainstalovaná SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="8c9e2-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="8c9e2-288">Aplikace, které zahrnují SQL Server Compact databáze, mohou běžet v počítači, kde není nainstalován SQL Server Compact.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="8c9e2-289">Microsoft WebMatrix beta 3 automaticky zkopíruje tyto binární soubory a provede příslušné transformace souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="8c9e2-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="8c9e2-290">**Alternativní řešení** Pokud potřebujete tyto soubory zkopírovat a provést změny v souboru *Web. config* ručně, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="8c9e2-291">Zkopírujte sestavení databázového stroje do složky *bin* (a podsložek) aplikace v cílovém počítači:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="8c9e2-292">Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.data.SqlServerCe.dll* **do** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="8c9e2-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="8c9e2-293">Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* \* **do** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="8c9e2-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="8c9e2-294">Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \* **do** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="8c9e2-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="8c9e2-295">V kořenové složce webu vytvořte nebo otevřete soubor *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="8c9e2-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="8c9e2-296">(Ve WebMatrixu beta 3 je tento typ souboru k dispozici, pokud kliknete na tlačítko **vše** v dialogovém okně **zvolit typ souboru** .)</span><span class="sxs-lookup"><span data-stu-id="8c9e2-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="8c9e2-297">Přidejte následující prvek jako podřízený prvek **&lt;konfigurace&gt;** (není uvnitř elementu **&lt;system. Web&gt;** ):</span><span class="sxs-lookup"><span data-stu-id="8c9e2-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="8c9e2-298">Problém: pomocníka databáze a WebGrid nefungují v nestředním vztahu důvěryhodnosti v Visual Basic</span><span class="sxs-lookup"><span data-stu-id="8c9e2-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="8c9e2-299">Pokud používáte Visual Basic (vytváření souborů *. vbhtml* ), `Database` a `WebGrid` pomocníka nebudou fungovat, pokud je aplikace nastavená tak, aby používala střední důvěryhodnost.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="8c9e2-300">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-300">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-301">Dočasně nastavte aplikaci tak, aby používala úplný vztah důvěryhodnosti.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="8c9e2-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="8c9e2-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="8c9e2-303">Problém: vlastnost Encrypt není rozpoznaná.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="8c9e2-304">SQL Server Compact 4,0 nerozpozná vlastnost `Encrypt` třídy `SqlCeConnection`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="8c9e2-305">Tuto vlastnost byste neměli používat k šifrování souborů databáze.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="8c9e2-306">Vlastnost `Encrypt` se v SQL Server Compact 3,5 verze nepoužívá a byla zachována pouze z důvodu zpětné kompatibility.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="8c9e2-307">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-307">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-308">Pomocí vlastnosti `Encryption Mode` třídy `SqlCeConnection` Zašifrujte soubory databáze SQL Server Compact 4,0.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="8c9e2-309">Následující příklad ukazuje, jak vytvořit šifrované databáze SQL Server Compact 4,0 pomocí vlastnosti `Encryption Mode`:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="8c9e2-310">Chcete-li změnit režim šifrování existující databáze SQL Server Compact 4,0, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="8c9e2-311">K šifrování nešifrované databáze SQL Server Compact 4,0 postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="8c9e2-312">Problém: vyžadují se C++ knihovny modulu runtime Microsoft Visual 2008.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="8c9e2-313">Nativní knihovny DLL SQL Server Compact 4,0 potřebují knihovny runtime Microsoft Visual C++ 2008 (x86, IA64 a x64) s aktualizací Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="8c9e2-314">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-314">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-315">Nainstalujte .NET Framework 3,5 SP1.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="8c9e2-316">Tím se také nainstaluje knihovny C++ Runtime Visual 2008 runtime SP1.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="8c9e2-317">Knihovny si můžete stáhnout z následujícího umístění:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="8c9e2-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package aktualizace zabezpečení knihovny ATL</span><span class="sxs-lookup"><span data-stu-id="8c9e2-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="8c9e2-319">Všimněte si, že při instalaci .NET Framework 2,0, 3,0 nebo 4 *se neinstalují* knihovny C++ runtime Visual 2008 SP1.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="8c9e2-320">Problém: Pokud je SQL Server Compact nainstalován před instalací nástroje .NET Framework na počítači, není v souboru .NET Framework Machine. config registrován jeho neutrální název poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="8c9e2-321">SQL Server Compact lze nainstalovat do počítače, který nemá .NET Framework nainstalován, protože SQL Server Compact vyžaduje rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="8c9e2-322">Pokud před instalací SQL Server Compact není nainstalovaná žádná .NET Framework verze 3,5 ani 4, instalační program SQL Server Compact neregistruje v souboru *Machine. config* jeho nevariantní poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="8c9e2-323">Žádná aplikace, která spoléhá na položku SQL Server Compact v souboru *Machine. config* , se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="8c9e2-324">Položka registrace neutrálního názvu v *souboru Machine. config* vypadá jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="8c9e2-325">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-325">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-326">Odinstalujte SQL Server Compact 4,0 CTP1.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="8c9e2-327">Z následujícího umístění si stáhněte a nainstalujte plné verze .NET Framework:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="8c9e2-328">Microsoft .NET Framework 3,5 Service Pack 1 (úplný balíček)</span><span class="sxs-lookup"><span data-stu-id="8c9e2-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="8c9e2-329">Verze Microsoft .NET Framework 4,0 (úplný balíček)</span><span class="sxs-lookup"><span data-stu-id="8c9e2-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="8c9e2-330">Pak přeinstalujte [SQL Server Compact 4,0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="8c9e2-331">Instalace aplikací</span><span class="sxs-lookup"><span data-stu-id="8c9e2-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="8c9e2-332">Problém: instalace aplikace může trvat dlouhou dobu, pokud se složka Dokumenty uživatele přesměruje na sdílenou síťovou složku.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="8c9e2-333">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-333">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-334">Žádné.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-334">None.</span></span> <span data-ttu-id="8c9e2-335">Instalace aplikace může nějakou dobu trvat, ale nainstaluje se správně.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-335">The application might take a while to install, but will install correctly.</span></span>

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="8c9e2-336">Publikování aplikací</span><span class="sxs-lookup"><span data-stu-id="8c9e2-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="8c9e2-337">Problém: po publikování nemusí lokalita fungovat, pokud se v poli Cílová adresa URL nepoužívá předpona http://nebo https://.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="8c9e2-338">Pokud v dialogovém okně **Nastavení publikování** nezačíná cílová adresa URL `http://` nebo `https://`, web po nasazení nemusí fungovat.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="8c9e2-339">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-339">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-340">Ujistěte se, že před publikováním webu se v dialogovém okně **Nastavení publikování** spustí cílová adresa URL s `http://` nebo `https://`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="8c9e2-341">Problém: publikování databáze MySQL se nepovede kvůli chybě: publikování databáze se nepovedlo.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="8c9e2-342">K tomu může dojít, pokud Vzdálená databáze nemůže skript spustit. "</span><span class="sxs-lookup"><span data-stu-id="8c9e2-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="8c9e2-343">K této chybě může dojít z několika důvodů.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="8c9e2-344">Jedním z důvodů, proč se tato chyba zobrazuje, je, že databázový skript obsahuje znak jednoduché uvozovky (') a výchozí znaková sada databáze MySQL není UTF-8.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="8c9e2-345">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-345">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-346">Nastavte výchozí znakovou sadu pro vzdálenou databázi MySQL na UTF-8.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="8c9e2-347">Další problémy</span><span class="sxs-lookup"><span data-stu-id="8c9e2-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="8c9e2-348">Problém: v sestavách pro Group by nefunguje hledání nebo filtr: typ problému</span><span class="sxs-lookup"><span data-stu-id="8c9e2-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="8c9e2-349">Pokud spustíte sestavu pro lokalitu, zadáte text do pole *filtrovat podle adresy URL* a kliknete na tlačítko *Hledat*, nic se nestane.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="8c9e2-350">Důvodem je to, že tento ovládací prvek není funkční, pokud je stav *Seskupit podle* sestavy nastaven na *typ vystavení*, což je výchozí hodnota.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="8c9e2-351">**Alternativní řešení** Na kartě *Seskupit podle* na pásu karet klikněte na možnost *Adresa URL* a seskupte položky podle jejich zdrojové adresy URL.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="8c9e2-352">Textové pole a tlačítko pro filtrování položek je funkční v tomto stavu.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-352">The text box and button to filter the entries are functional while in this state.</span></span>

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="8c9e2-353">Problém: aplikace WCF selhaly při spuštění s IIS Express</span><span class="sxs-lookup"><span data-stu-id="8c9e2-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="8c9e2-354">Při procházení aplikace WCF dojde k chybě podobné následujícímu:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="8c9e2-355">*Nelze načíst soubor nebo sestavení Microsoft. Web. Administration, Version = 7.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 nebo jedna z jejích závislostí. Systém nemůže najít zadaný soubor.*</span><span class="sxs-lookup"><span data-stu-id="8c9e2-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="8c9e2-356">K tomu dochází, protože IIS Express beta verze standardně nepodporuje WCF.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="8c9e2-357">**Alternativní řešení** Použijte jedno z následujících řešení (alternativní řešení #2 vyžaduje Microsoft Windows Vista nebo novější):</span><span class="sxs-lookup"><span data-stu-id="8c9e2-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="8c9e2-358">Zkopírujte sestavení *Microsoft. Web. dll* a *Microsoft. Web. Administration. dll* z umístění instalace WebMatrix do adresáře *bin* aplikace WCF.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="8c9e2-359">Ve výchozím nastavení je WebMatrix nainstalovaný v podsložce *WebMatrixu Microsoftu* ve složce *Program Files (Program Files* ) systému.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="8c9e2-360">V systému Microsoft Windows Vista nebo novějším vytvořte symlink do sestavení v adresáři *bin* pomocí následujících příkazů.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="8c9e2-361">(Tento přístup má výhodu, že nevytváří kopii sestavení.)</span><span class="sxs-lookup"><span data-stu-id="8c9e2-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="8c9e2-362">Nainstalujte dvě sestavení v globální mezipaměti sestavení (GAC).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="8c9e2-363">Na příkazovém řádku se zvýšenými oprávněními spusťte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="8c9e2-364">Problém: WebMatrix beta 3 není schopen provádět určité úlohy, které vyžadují zvýšení úrovně oprávnění.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="8c9e2-365">WebMatrix beta 3 není schopen provádět určité úlohy, které vyžadují zvýšení oprávnění, jako je například instalace dalších součástí v následujících situacích:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="8c9e2-366">V systému Windows Vista nebo Windows 7 jste přihlášeni pomocí účtu, který nemá oprávnění správce a nástroj řízení uživatelských účtů (UAC) je zakázán.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="8c9e2-367">Používáte Microsoft Windows XP nebo Microsoft Windows Server 2003.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="8c9e2-368">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-368">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-369">Většina úkolů v WebMatrixu beta 3 nevyžaduje oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="8c9e2-370">V případě, že to uděláte, můžete tuto operaci provést jako správce nebo postupovat podle následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="8c9e2-371">V systému Windows Vista nebo Windows 7 povolte nástroj řízení uživatelských účtů.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="8c9e2-372">V systému Windows XP přidejte uživatele do skupiny zabezpečení Správci.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-372">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="8c9e2-373">Problém: lokalita z webové galerie je zakázaná.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="8c9e2-374">Možnost **web z Galerie webu** je zakázána, pokud není nainstalována instalace webové platformy 3,0.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="8c9e2-375">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-375">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-376">Nainstalujte [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="8c9e2-377">Problém: v systému Windows Server 2003 se IIS Express nespouštějí pro uživatele bez oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="8c9e2-378">Pokud na Windows serveru 2003 spustíte stránku nebo spustíte IIS Express, IIS Express se nespustí.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="8c9e2-379">U webových stránek se zobrazí chyba, která indikuje, že aplikace byla spuštěna uživatelem bez oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="8c9e2-380">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-380">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-381">Spusťte WebMatrix beta 3 jako uživatel s právy pro správu.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="8c9e2-382">Další podrobnosti najdete v následujícím článku znalostní báze:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="8c9e2-383">Aplikace, kterou spouští uživatel bez oprávnění správce, nemůže naslouchat přenosu HTTP počítače, na kterém je aplikace spuštěná v systému Windows Vista, Windows Server 2003 nebo Windows XP.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="8c9e2-384">Problém: Google Chrome není k dispozici jako možnost spuštění.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="8c9e2-385">Google Chrome se v seznamu **Spustit** na kartě **Domů** nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="8c9e2-386">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-386">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-387">Některé verze Google Chrome se neregistrují správně s funkcí výchozí programy v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="8c9e2-388">Jako alternativní řešení spusťte Google Chrome, klikněte na nabídku *přizpůsobit a řídit Google Chrome* , klikněte na *Možnosti*a potom klikněte na *nastavit Google Chrome výchozí prohlížeč*.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="8c9e2-389">Problém: dialogové okno cizí klíč nepovoluje zadávání primárního klíče.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="8c9e2-390">Dialogové okno **cizí klíč** vám neumožňuje zadat název primárního klíče z tabulky primárního klíče.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="8c9e2-391">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-391">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-392">To je úmyslné.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-392">This is intentional.</span></span> <span data-ttu-id="8c9e2-393">Nemusíte zadávat název primárního klíče z tabulky primárního klíče.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-393">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="8c9e2-394">Problém: tlačítko relace je zakázané.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="8c9e2-395">Tlačítko **relace** na kartě **tabulka** v pracovním prostoru **databáze** je pro databáze SQL Server Compact zakázané.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="8c9e2-396">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-396">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-397">Žádné.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-397">None.</span></span> <span data-ttu-id="8c9e2-398">SQL Server Compact nepodporuje relace mezi tabulkami.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-398">SQL Server Compact does not support relationships between tables.</span></span>

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="8c9e2-399">Problém: parametrizované dotazy SQL vyvolávají výjimky</span><span class="sxs-lookup"><span data-stu-id="8c9e2-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="8c9e2-400">Pokud v SQL Server Compact 4,0 neurčíte datový typ, například `SqlDbType` nebo `DbType` pro parametry v parametrizovaných dotazech, je vyvolána výjimka při spuštění dotazu.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="8c9e2-401">**Alternativní řešení**</span><span class="sxs-lookup"><span data-stu-id="8c9e2-401">**Workaround**</span></span>  
> <span data-ttu-id="8c9e2-402">Explicitně nastavte datový typ pro parametry, jako je `SqlDbType` nebo `DbType`.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="8c9e2-403">To je důležité v případě datových typů objektů BLOB (`image` a `ntext`).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="8c9e2-404">Použijte kód podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="8c9e2-405">Další informace</span><span class="sxs-lookup"><span data-stu-id="8c9e2-405">For More Information</span></span>

<span data-ttu-id="8c9e2-406">Další informace o WebMatrixu beta 3 najdete na následujících webech:</span><span class="sxs-lookup"><span data-stu-id="8c9e2-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="8c9e2-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="8c9e2-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="8c9e2-408">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8c9e2-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="8c9e2-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="8c9e2-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

---

<span data-ttu-id="8c9e2-410">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="8c9e2-411">Všechna práva vyhrazena.</span><span class="sxs-lookup"><span data-stu-id="8c9e2-411">All Rights Reserved.</span></span> <span data-ttu-id="8c9e2-412">[Podmínek použití](https://msdn.microsoft.cos/cc300389.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c9e2-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
