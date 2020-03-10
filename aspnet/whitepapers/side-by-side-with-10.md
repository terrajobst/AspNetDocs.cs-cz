---
uid: whitepapers/side-by-side-with-10
title: ASP.NET souběžného spouštění .NET Framework 1,0 a 1,1 | Microsoft Docs
author: rick-anderson
description: Tento dokument white paper popisuje, jak nainstalovat rozhraní .NET 1,0 i .NET 1,1 na váš počítač, což umožňuje spuštění webové aplikace v ASP.NET v obou verzích Fram...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632970"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="69c35-103">ASP.NET – souběžné spuštění .NET Framework 1.0 a 1.1</span><span class="sxs-lookup"><span data-stu-id="69c35-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>

> <span data-ttu-id="69c35-104">Tento dokument white paper popisuje, jak nainstalovat rozhraní .NET 1,0 i .NET 1,1 na váš počítač, což umožňuje spuštění webové aplikace v ASP.NET v obou verzích rozhraní.</span><span class="sxs-lookup"><span data-stu-id="69c35-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="69c35-105">Platí pro ASP.NET 1,0 a ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="69c35-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="69c35-106">V ASP.NET jsou aplikace označeny jako spuštěné souběžně, když jsou nainstalovány ve stejném počítači, ale používají různé verze .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69c35-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="69c35-107">Následující téma popisuje, jak nakonfigurovat aplikace ASP.NET pro souběžné spouštění a poskytuje podrobné kroky pro:</span><span class="sxs-lookup"><span data-stu-id="69c35-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="69c35-108">Udržovat mapování webové aplikace na verzi .NET Framework 1,0 během instalace</span><span class="sxs-lookup"><span data-stu-id="69c35-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="69c35-109">Mapování webové aplikace na konkrétní verzi .NET Framework</span><span class="sxs-lookup"><span data-stu-id="69c35-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="69c35-110">Vyhledání verze .NET Framework, kterou používá web</span><span class="sxs-lookup"><span data-stu-id="69c35-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="69c35-111">Tradičně platí, že při aktualizaci součásti nebo aplikace v počítači je starší verze odebrána a nahrazena novější verzí.</span><span class="sxs-lookup"><span data-stu-id="69c35-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="69c35-112">Pokud nová verze není kompatibilní s předchozí verzí, obvykle se tím přeruší jiné aplikace, které používají komponentu nebo aplikaci.</span><span class="sxs-lookup"><span data-stu-id="69c35-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="69c35-113">.NET Framework poskytuje podporu pro souběžné spouštění, které umožňuje nainstalovat více verzí sestavení nebo aplikace do stejného počítače současně.</span><span class="sxs-lookup"><span data-stu-id="69c35-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="69c35-114">Vzhledem k tomu, že je možné nainstalovat více verzí současně, můžou spravované aplikace vybrat, která verze se má použít, aniž by to ovlivnilo aplikace, které používají jinou verzi.</span><span class="sxs-lookup"><span data-stu-id="69c35-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="69c35-115">Ve výchozím nastavení se při instalaci .NET Framework verze 1,1 všechny existující aplikace ASP.NET automaticky překonfigurují tak, aby používaly nejnovější verzi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69c35-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="69c35-116">Pokud nechcete, aby se aplikace ASP.NET ve výchozím nastavení .NET Framework 1,1, kliknutím [sem](#1) se dozvíte, jak v průběhu instalace zabránit.</span><span class="sxs-lookup"><span data-stu-id="69c35-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="69c35-117">Pokud aktualizujete webový server na .NET Framework 1,1 a chcete, aby jedna nebo více webových aplikací běžela .NET Framework 1,0, je nutné aktualizovat mapu skriptů Internetová informační služba (IIS).</span><span class="sxs-lookup"><span data-stu-id="69c35-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="69c35-118">Mapování skriptu je mechanismus pro mapování přípony souboru. aspx pro konkrétní webovou aplikaci na verzi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69c35-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="69c35-119">Kliknutím [sem](#2) se dozvíte, jak namapovat webovou aplikaci na konkrétní verzi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69c35-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="69c35-120">K vyhledání, na které .NET Framework verze je spuštěná konkrétní webová aplikace, můžete použít nástroj pro registraci internetových informací nebo ASP.NET služby IIS (ASPNET\_regiis. exe).</span><span class="sxs-lookup"><span data-stu-id="69c35-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="69c35-121">Kliknutím [sem](#3) zjistíte, jak najít verzi .NET Framework, kterou používá web.</span><span class="sxs-lookup"><span data-stu-id="69c35-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="69c35-122">Jedním z importovaných aspektů při migraci na .NET Framework 1,1 je, že každá verze .NET Framework používá vlastní soubor Machine. config.</span><span class="sxs-lookup"><span data-stu-id="69c35-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="69c35-123">V důsledku toho, pokud webový správce provedl změny v souboru Machine. config, musí být tyto změny migrovány do souboru .NET Framework 1,1 Machine. config.</span><span class="sxs-lookup"><span data-stu-id="69c35-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="69c35-124">Údržba mapování webové aplikace na .NET Framework 1,0 během instalace</span><span class="sxs-lookup"><span data-stu-id="69c35-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="69c35-125">Ve výchozím nastavení se všechny existující aplikace ASP.NET při instalaci automaticky překonfigurují, aby používaly novější verzi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69c35-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="69c35-126">Pomocí novější verze .NET Framework můžou aplikace plně využívat vylepšení a nové funkce, které jsou součástí nové verze.</span><span class="sxs-lookup"><span data-stu-id="69c35-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="69c35-127">Zároveň správce webu, který může chtít podrobnou kontrolu nad tím, které aplikace se aktualizují, může zabránit automatickému přemapování všech stávajících aplikací ASP.NET během instalace .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69c35-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="69c35-128">Chcete-li zabránit automatickému přemapování celé aplikace ASP.NET na novější verzi .NET Framework, může správce webu použít možnost příkazového řádku/noaspupgrade s instalačním programem Dotnetfx. exe.</span><span class="sxs-lookup"><span data-stu-id="69c35-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="69c35-129">**Zamezení úplného přemapování aplikace ASP.NET na novější verzi**</span><span class="sxs-lookup"><span data-stu-id="69c35-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="69c35-130">Přejít na **začátek**.</span><span class="sxs-lookup"><span data-stu-id="69c35-130">Go to **Start**.</span></span>
2. <span data-ttu-id="69c35-131">Klikněte na **Spustit**.</span><span class="sxs-lookup"><span data-stu-id="69c35-131">Click on **run**.</span></span>
3. <span data-ttu-id="69c35-132">Zadejte **příkaz cmd**.</span><span class="sxs-lookup"><span data-stu-id="69c35-132">Type **cmd**.</span></span>
4. <span data-ttu-id="69c35-133">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="69c35-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="69c35-134">Na příkazovém řádku zadejte následující řádek, který spustí instalaci .NET Framework: **Dotnetfx. exe/c: "Install/noaspupgrade?** .</span><span class="sxs-lookup"><span data-stu-id="69c35-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="69c35-135">V instalačním programu Microsoft .NET Framework 1,1 klikněte na **Ano** .</span><span class="sxs-lookup"><span data-stu-id="69c35-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="69c35-136">Tím se spustí proces instalace .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="69c35-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="69c35-137">Mapování webové aplikace na konkrétní verzi .NET Framework</span><span class="sxs-lookup"><span data-stu-id="69c35-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="69c35-138">Každá verze .NET Framework zahrnuje verzi registračního nástroje ASP.NET služby IIS (ASPNET\_regiis. exe).</span><span class="sxs-lookup"><span data-stu-id="69c35-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="69c35-139">Tento nástroj umožňuje správcům určit, že webová aplikace bude spuštěna v konkrétní verzi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69c35-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="69c35-140">To se označuje jako mapování webové aplikace na verzi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="69c35-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="69c35-141">Správci musí vybrat soubor ASPNET\_regiis. exe, který odpovídá verzi .NET Framework, která bude přidružena k webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="69c35-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="69c35-142">Například správce, který chce určit, aby web používal .NET Framework 1,1, musí použít soubor ASPNET\_regiis. exe, který je součástí .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="69c35-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="69c35-143">ASPNET\_regiis. exe pro verzi 1,0 se nachází v:</span><span class="sxs-lookup"><span data-stu-id="69c35-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="69c35-144">C:\WINDOWS\Microsoft.NET\Framework\\**v 1.0.3705**\ASPNET\_regiis</span><span class="sxs-lookup"><span data-stu-id="69c35-144">C:\WINDOWS\Microsoft.NET\Framework\\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="69c35-145">ASPNET\_regiis. exe pro verzi 1, 1 je umístěn v:</span><span class="sxs-lookup"><span data-stu-id="69c35-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="69c35-146">C:\WINDOWS\Microsoft.NET\Framework\\**v 1.1.4322**\ASPNET\_regiis</span><span class="sxs-lookup"><span data-stu-id="69c35-146">C:\WINDOWS\Microsoft.NET\Framework\\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="69c35-147">ASPNET\_regiis. exe poskytuje dvě možnosti mapování skriptu webové aplikace:</span><span class="sxs-lookup"><span data-stu-id="69c35-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="69c35-148">**-s** Nastaví mapu skriptu v cestě a v jejích podřízených adresářích.</span><span class="sxs-lookup"><span data-stu-id="69c35-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="69c35-149">**-sn** Nastaví mapu skriptu pouze v cestě.</span><span class="sxs-lookup"><span data-stu-id="69c35-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="69c35-150">Cesta definuje cestu metadat služby IIS webové aplikace, která je definovaná ve formě W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span><span class="sxs-lookup"><span data-stu-id="69c35-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="69c35-151">Například pro webovou aplikaci s názvem portál umístěný na výchozím webu je cesta metabáze W3SVC/1/ROOT/Portal.</span><span class="sxs-lookup"><span data-stu-id="69c35-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="69c35-152">Poznámka: k získání cesty k metabázi můžete použít také nástroj nazvaný Editor metabáze.</span><span class="sxs-lookup"><span data-stu-id="69c35-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="69c35-153">Tento nástroj si můžete stáhnout z webu podpora Microsoftu na [https://support.microsoft.com/default.aspx?scid=kb; en-US; 232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span><span class="sxs-lookup"><span data-stu-id="69c35-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="69c35-154">Spuštěním ASPNET\_regiis. exe-s W3SVC/1/ROOT/Portal aktualizujte mapu skriptů služby IIS portálu a její podaplikaci.</span><span class="sxs-lookup"><span data-stu-id="69c35-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="69c35-155">Spuštěním ASPNET\_regiis. exe-SN W3SVC/1/ROOT/Portal aktualizujte mapu skriptů služby IIS portálu, aniž by to ovlivnilo aplikace v podadresářích portálu.</span><span class="sxs-lookup"><span data-stu-id="69c35-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="69c35-156">Najít .NET Framework verzi, kterou webová aplikace používá</span><span class="sxs-lookup"><span data-stu-id="69c35-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="69c35-157">Správce může použít Service Manager internetu k nalezení verze .NET Framework, na které běží Web.</span><span class="sxs-lookup"><span data-stu-id="69c35-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="69c35-158">Různé verze operačního systému spouštějí Internet Service Manager odlišně.</span><span class="sxs-lookup"><span data-stu-id="69c35-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="69c35-159">Chcete-li spustit nástroj Service Manager, postupujte podle kroků uvedených níže.</span><span class="sxs-lookup"><span data-stu-id="69c35-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="69c35-160">**Spuštění Service Manager Internetu**</span><span class="sxs-lookup"><span data-stu-id="69c35-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="69c35-161">Přejít na **začátek**.</span><span class="sxs-lookup"><span data-stu-id="69c35-161">Go to **Start**.</span></span>
2. <span data-ttu-id="69c35-162">Klikněte na **Spustit**.</span><span class="sxs-lookup"><span data-stu-id="69c35-162">Click on **run**.</span></span>
3. <span data-ttu-id="69c35-163">Zadejte **inetmgr**.</span><span class="sxs-lookup"><span data-stu-id="69c35-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="69c35-164">Z Service Manager Internetu vyberte webovou aplikaci, jejíž verze .NET Framework chcete znát.</span><span class="sxs-lookup"><span data-stu-id="69c35-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="69c35-165">Klikněte pravým tlačítkem na webovou aplikaci a pak klikněte na **Vlastnosti.**</span><span class="sxs-lookup"><span data-stu-id="69c35-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="69c35-166">V okně vlastností vyberte **konfigurace.**</span><span class="sxs-lookup"><span data-stu-id="69c35-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="69c35-167">V tabulce mapování aplikace vyberte **. aspx**a klikněte na **Upravit**.</span><span class="sxs-lookup"><span data-stu-id="69c35-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="69c35-168">V textovém poli **spustitelný soubor** vyhledejte v adresáři verze posouváním.</span><span class="sxs-lookup"><span data-stu-id="69c35-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="69c35-169">Pokud je adresář verze v. 1.1.4322, aplikace je namapována na .NET Framework 1,1.</span><span class="sxs-lookup"><span data-stu-id="69c35-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="69c35-170">Naopak, pokud je adresář verze v 1.0.3705, aplikace je namapována na .NET Framework 1,0.</span><span class="sxs-lookup"><span data-stu-id="69c35-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
