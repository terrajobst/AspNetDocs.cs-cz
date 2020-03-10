---
uid: whitepapers/aspnet-and-iis6
title: Spuštění ASP.NET 1,1 se službou IIS 6,0 | Microsoft Docs
author: rick-anderson
description: Systém Windows Server 2003 zahrnuje službu IIS 6,0 i ASP.NET 1,1. tyto komponenty jsou ve výchozím nastavení zakázány. Tento dokument white paper popisuje, jak povolit IIS 6,0...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523308"
---
# <a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="c7660-104">Spuštění ASP.NET 1.1 se službou IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="c7660-104">Running ASP.NET 1.1 with IIS 6.0</span></span>

> <span data-ttu-id="c7660-105">Systém Windows Server 2003 zahrnuje službu IIS 6,0 i ASP.NET 1,1. tyto komponenty jsou ve výchozím nastavení zakázány.</span><span class="sxs-lookup"><span data-stu-id="c7660-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="c7660-106">Tento dokument white paper popisuje, jak povolit IIS 6,0 a ASP.NET 1,1 a doporučuje několik nastavení konfigurace, aby se dosáhlo optimálního výkonu služeb IIS a ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c7660-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="c7660-107">Platí pro ASP.NET 1,1 a IIS 6,0.</span><span class="sxs-lookup"><span data-stu-id="c7660-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>

<span data-ttu-id="c7660-108">ASP.NET 1,1 dodává se systémem Windows Server 2003, který obsahuje také nejnovější verzi serveru Internet Information Server (IIS) 6,0.</span><span class="sxs-lookup"><span data-stu-id="c7660-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="c7660-109">Služba IIS 6,0 a ASP.NET 1,1 jsou navržené tak, aby se hladce integrují a ASP.NET teď ve výchozím nastavení nový model pracovních procesů služby IIS 6,0.</span><span class="sxs-lookup"><span data-stu-id="c7660-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="c7660-110">ASP.NET 1,1 není ve výchozím nastavení nainstalovaná.</span><span class="sxs-lookup"><span data-stu-id="c7660-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="c7660-111">Na rozdíl od předchozích verzí operačních systémů serveru společnosti Microsoft není služba Internet Information Server (IIS) standardně povolena. ani ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="c7660-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="c7660-112">Existují dvě možnosti, jak povolit službu IIS:</span><span class="sxs-lookup"><span data-stu-id="c7660-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="c7660-113">Povolení služby IIS, možnosti #1 – Průvodce konfigurací serveru</span><span class="sxs-lookup"><span data-stu-id="c7660-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="c7660-114">Windows Server 2003 dodává nový průvodce konfigurací serveru, který vám umožní správně nakonfigurovat server v požadovaném režimu.</span><span class="sxs-lookup"><span data-stu-id="c7660-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="c7660-115">Chcete-li spustit Průvodce – Poznámka: Chcete-li spustit průvodce, je nutné, abyste byli přihlášeni jako správce – přejít na: Start | Programy | Nástroje pro správu a vyberte Konfigurovat Server.</span><span class="sxs-lookup"><span data-stu-id="c7660-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="c7660-116">Po výběru byste měli vidět úvodní obrazovku průvodce konfigurací serveru:</span><span class="sxs-lookup"><span data-stu-id="c7660-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="c7660-117">Klikněte na další &gt;:</span><span class="sxs-lookup"><span data-stu-id="c7660-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="c7660-118">Klikněte na další &gt;.</span><span class="sxs-lookup"><span data-stu-id="c7660-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="c7660-119">Na této obrazovce budete muset jako možnosti konfigurace vybrat aplikační server (IIS, ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="c7660-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="c7660-120">Klikněte na tlačítko Další &gt;.</span><span class="sxs-lookup"><span data-stu-id="c7660-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="c7660-121">Po výběru konfigurace serveru jako aplikačního serveru se zobrazí tato obrazovka s výzvou k tomu, jaké další možnosti by se měly nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="c7660-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="c7660-122">Ve výchozím nastavení není vybraná žádná možnost.</span><span class="sxs-lookup"><span data-stu-id="c7660-122">Neither option is selected by default.</span></span> <span data-ttu-id="c7660-123">Pokud chcete ASP.NET povolit automaticky, musíte vybrat Povolit ASP. NET.</span><span class="sxs-lookup"><span data-stu-id="c7660-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="c7660-124">Klikněte na tlačítko Další &gt;.</span><span class="sxs-lookup"><span data-stu-id="c7660-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="c7660-125">Tato obrazovka zobrazuje, jaké možnosti se mají nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="c7660-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="c7660-126">Klikněte na tlačítko Další &gt;.</span><span class="sxs-lookup"><span data-stu-id="c7660-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="c7660-127">Tato obrazovka se zobrazí při instalaci možností, které jste vybrali.</span><span class="sxs-lookup"><span data-stu-id="c7660-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="c7660-128">V normálním případě se zobrazí další dialogová okna, která se instalují jako služby.</span><span class="sxs-lookup"><span data-stu-id="c7660-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="c7660-129">Může se zobrazit také výzva k zadání umístění instalačního disku CD systému Windows 2003 Server.</span><span class="sxs-lookup"><span data-stu-id="c7660-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="c7660-130">Po dokončení klikněte na tlačítko ' další &gt;'.</span><span class="sxs-lookup"><span data-stu-id="c7660-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="c7660-131">Klikněte na Dokončit – Windows Server 2003 je teď nakonfigurovaný tak, aby podporoval IIS 6,0 a ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="c7660-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="c7660-132">Povolení služby IIS, možnost #2 – Ruční konfigurace služby IIS a ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c7660-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="c7660-133">Pokud nechcete používat Průvodce konfigurací serveru, můžete volitelně nainstalovat IIS 6,0 a ASP.NET 1,1 pomocí příkazu Přidat nebo odebrat programy v Ovládacích panelech.</span><span class="sxs-lookup"><span data-stu-id="c7660-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="c7660-134">Nejprve otevřete ovládací panely:</span><span class="sxs-lookup"><span data-stu-id="c7660-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="c7660-135">Potom klikněte na tlačítko Přidat nebo odebrat součásti systému Windows. otevře se Průvodce součástmi systému Windows:</span><span class="sxs-lookup"><span data-stu-id="c7660-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="c7660-136">Zvýrazněte a zkontrolujte aplikační server a pak klikněte na podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="c7660-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="c7660-137">tlačítko</span><span class="sxs-lookup"><span data-stu-id="c7660-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="c7660-138">Pokud chcete nainstalovat ASP.NET, podívejte se na ASP. NET.</span><span class="sxs-lookup"><span data-stu-id="c7660-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="c7660-139">Kliknutím na tlačítko OK se vraťte do Průvodce součástmi systému Windows.</span><span class="sxs-lookup"><span data-stu-id="c7660-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="c7660-140">Spusťte instalaci kliknutím na tlačítko Další &gt;v Průvodci součástmi systému Windows:</span><span class="sxs-lookup"><span data-stu-id="c7660-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="c7660-141">V normálním případě se zobrazí další dialogová okna, která se instalují jako služby.</span><span class="sxs-lookup"><span data-stu-id="c7660-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="c7660-142">Může se zobrazit také výzva k zadání umístění instalačního disku CD systému Windows 2003 Server.</span><span class="sxs-lookup"><span data-stu-id="c7660-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="c7660-143">Po dokončení instalace se zobrazí poslední obrazovka Průvodce součástmi systému Windows:</span><span class="sxs-lookup"><span data-stu-id="c7660-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="c7660-144">Služba IIS 6,0 a ASP.NET 1,1 jsou teď nakonfigurované a dostupné.</span><span class="sxs-lookup"><span data-stu-id="c7660-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="c7660-145">Doporučené nastavení</span><span class="sxs-lookup"><span data-stu-id="c7660-145">Recommended Settings</span></span>

<span data-ttu-id="c7660-146">Při spuštění ASP.NET 1,1 se službou IIS 6,0 je k dispozici několik nastavení konfigurace, která jsou doporučena k dosažení optimálního výkonu z ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="c7660-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="c7660-147">Konfigurace omezení paměti pracovních procesů</span><span class="sxs-lookup"><span data-stu-id="c7660-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="c7660-148">Konfigurace recyklace pracovních procesů</span><span class="sxs-lookup"><span data-stu-id="c7660-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="c7660-149">Konfigurace omezení paměti pracovních procesů</span><span class="sxs-lookup"><span data-stu-id="c7660-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="c7660-150">Ve výchozím nastavení služba IIS 6,0 nenastavuje omezení velikosti paměti, kterou může služba IIS používat.</span><span class="sxs-lookup"><span data-stu-id="c7660-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="c7660-151">Formátu. Funkce mezipaměti netto spoléhá na omezení paměti, takže mezipaměť může proaktivně odebrat nepoužívané položky z paměti.</span><span class="sxs-lookup"><span data-stu-id="c7660-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="c7660-152">Doporučuje se nakonfigurovat funkci Recyklace paměti služby IIS 6,0.</span><span class="sxs-lookup"><span data-stu-id="c7660-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="c7660-153">Konfigurace tohoto programu Open Internetová informační služba Manager (Start | Programy | Nástroje pro správu | Internetová informační služba).</span><span class="sxs-lookup"><span data-stu-id="c7660-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="c7660-154">Po otevření rozbalte složku fondy aplikací:</span><span class="sxs-lookup"><span data-stu-id="c7660-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="c7660-155">Pro každý fond aplikací:</span><span class="sxs-lookup"><span data-stu-id="c7660-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="c7660-156">Klikněte pravým tlačítkem na fond aplikací, třeba DefaultAppPool, a vyberte vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="c7660-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="c7660-157">Potom kliknutím na možnost maximální velikost využité paměti (v megabajtech) Povolte recyklaci paměti:.</span><span class="sxs-lookup"><span data-stu-id="c7660-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="c7660-158">Hodnota by neměla být větší než velikost fyzické (ne virtuální) paměti na serveru, dobrý odhad je 60% fyzické paměti, tj. pro server s 512 MB fyzické paměti vyberte 310.</span><span class="sxs-lookup"><span data-stu-id="c7660-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="c7660-159">Doporučuje se také, aby při použití 2 GB adresního prostoru nepřekročila maximální počet 800MB.</span><span class="sxs-lookup"><span data-stu-id="c7660-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="c7660-160">Pokud je adresní prostor paměti serveru povolenou, maximální limit paměti pro pracovní proces může být vysoký jako 1, 800MB:</span><span class="sxs-lookup"><span data-stu-id="c7660-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="c7660-161">Kliknutím na Apply (použít) a kliknutím na OK zavřete dialogové okno Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="c7660-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="c7660-162">Tento postup opakujte pro všechny dostupné fondy aplikací.</span><span class="sxs-lookup"><span data-stu-id="c7660-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="c7660-163">Konfigurace recyklace pracovních procesů</span><span class="sxs-lookup"><span data-stu-id="c7660-163">Configuring worker recycling</span></span>

<span data-ttu-id="c7660-164">Ve výchozím nastavení je služba IIS 6,0 nakonfigurovaná k recyklaci pracovního procesu každých 29 hodin.</span><span class="sxs-lookup"><span data-stu-id="c7660-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="c7660-165">Toto je trochu agresivní aplikace běžící na ASP.NET a doporučuje se, aby se automatické recyklace pracovních procesů zakázala.</span><span class="sxs-lookup"><span data-stu-id="c7660-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="c7660-166">Chcete-li zakázat automatickou recyklaci pracovních procesů, otevřete nejprve správce Internetová informační služba (Start | Programy | Nástroje pro správu | Internetová informační služba).</span><span class="sxs-lookup"><span data-stu-id="c7660-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="c7660-167">Po otevření rozbalte složku fondy aplikací:</span><span class="sxs-lookup"><span data-stu-id="c7660-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="c7660-168">Pro každý fond aplikací:</span><span class="sxs-lookup"><span data-stu-id="c7660-168">For each application pool:</span></span>

1. <span data-ttu-id="c7660-169">Klikněte pravým tlačítkem na fond aplikací, třeba DefaultAppPool, a vyberte vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="c7660-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="c7660-170">Zrušit kontrolu pracovního procesu recyklace (v minutách): ':</span><span class="sxs-lookup"><span data-stu-id="c7660-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="c7660-171">Kliknutím na Apply (použít) a kliknutím na OK zavřete dialogové okno Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="c7660-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="c7660-172">Tento postup opakujte pro všechny dostupné fondy aplikací.</span><span class="sxs-lookup"><span data-stu-id="c7660-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="c7660-173">Udělení přístupu pro zápis do systému souborů</span><span class="sxs-lookup"><span data-stu-id="c7660-173">Granting write access to the file system</span></span>

<span data-ttu-id="c7660-174">Pokud vaše aplikace vyžaduje oprávnění k zápisu do systému souborů a používáte systém souborů NTFS, budete muset upravit seznam Access Control (ACL) pro složku nebo soubor a udělit tak přístup k ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c7660-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="c7660-175">Pokud například chcete udělit přístup pro zápis ASP.NET do složky c:\Inetpub\Wwwroot, otevřete Průzkumníka a přejděte do adresáře:</span><span class="sxs-lookup"><span data-stu-id="c7660-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="c7660-176">Potom klikněte pravým tlačítkem na adresář, třeba na "wwwroot" a vyberte vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="c7660-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="c7660-177">Po otevření dialogového okna Vlastnosti vyberte kartu zabezpečení:</span><span class="sxs-lookup"><span data-stu-id="c7660-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="c7660-178">Adresář c:\InetPub\Wwwroot\ je speciální adresář v tom, že speciální skupina služby IIS 6,0, kterou služba IIS\_WPG, už má udělenou možnost číst &amp; spouštění, zobrazovat obsah složky a číst.</span><span class="sxs-lookup"><span data-stu-id="c7660-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="c7660-179">Pokud ale chcete udělit oprávnění k zápisu, musíte kliknout na zaškrtávací políčko Povolit pro zápis:</span><span class="sxs-lookup"><span data-stu-id="c7660-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="c7660-180">Služba IIS 6,0 má teď oprávnění k zápisu do této složky.</span><span class="sxs-lookup"><span data-stu-id="c7660-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="c7660-181">Pokud chcete udělit oprávnění k zápisu na jiné složky, postupujte podle těchto kroků – Poznámka: Pokud ještě neexistuje, možná budete muset přidat skupinu IIS\_WPG.</span><span class="sxs-lookup"><span data-stu-id="c7660-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="c7660-182">Udělení oprávnění k zápisu do služby IIS\_WPG umožní zapisovat do tohoto adresáře všechny aplikace v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c7660-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="c7660-183">Podpora integrovaného ověřování pomocí SQL Server</span><span class="sxs-lookup"><span data-stu-id="c7660-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="c7660-184">Integrované ověřování umožňuje SQL Server využívat ověřování systému Windows NT k ověření účtů přihlášení SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c7660-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="c7660-185">Uživatel tak může obejít standardní SQL Server procesu přihlášení.</span><span class="sxs-lookup"><span data-stu-id="c7660-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="c7660-186">Pomocí tohoto přístupu může uživatel sítě získat přístup k databázi SQL Server bez zadání samostatného přihlašovacího ID nebo hesla, protože SQL Server získá informace o uživateli a heslech z procesu zabezpečení sítě systému Windows NT.</span><span class="sxs-lookup"><span data-stu-id="c7660-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="c7660-187">Volba integrovaného ověřování pro aplikace ASP.NET je dobrá volba, protože v připojovacím řetězci nejsou někdy uloženy žádné přihlašovací údaje pro vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="c7660-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="c7660-188">Místo toho se připojovací řetězec použitý k připojení k SQL bude podobat následujícímu:</span><span class="sxs-lookup"><span data-stu-id="c7660-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="c7660-189">Tento připojovací řetězec oznamuje SQL Server, aby používal přihlašovací údaje Windows pro aplikaci, která se pokouší získat přístup k SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c7660-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="c7660-190">V případě ASP.NET/IIS 6 by to byl účet ve skupině služby IIS\_WPG.</span><span class="sxs-lookup"><span data-stu-id="c7660-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="c7660-191">Pokud chcete povolit integrované ověřování mezi SQL Server a ASP.NET, musíte nejdřív zkontrolovat, jestli je SQL Server nakonfigurované pro integrované ověřování nebo ověřování ve smíšeném režimu – Pokud ho chcete zjistit, kontaktujte správce databáze.</span><span class="sxs-lookup"><span data-stu-id="c7660-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="c7660-192">Pokud je SQL Server v jednom z těchto dvou režimů, můžete použít integrované ověřování.</span><span class="sxs-lookup"><span data-stu-id="c7660-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="c7660-193">Otevřete správce SQL Server Enterprise (Start | Programy | Microsoft SQL Server | Enterprise Manager) vyberte příslušný server a rozbalte složku zabezpečení:</span><span class="sxs-lookup"><span data-stu-id="c7660-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="c7660-194">Pokud není uvedená skupina BUILTINT\IIS\_WPG, klikněte pravým tlačítkem na přihlašovací údaje a vyberte New Login:</span><span class="sxs-lookup"><span data-stu-id="c7660-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="c7660-195">Do textového pole název: zadejte [Server/název domény] \IIS\_WPG nebo klikněte na tlačítko se třemi tečkami a otevřete výběr uživatele nebo skupiny Windows NT:</span><span class="sxs-lookup"><span data-stu-id="c7660-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="c7660-196">Vyberte skupinu IIS\_aktuální počítač a kliknutím na tlačítko Přidat a OK zavřete výběr.</span><span class="sxs-lookup"><span data-stu-id="c7660-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="c7660-197">Pak je nutné nastavit také výchozí databázi a oprávnění pro přístup k databázi.</span><span class="sxs-lookup"><span data-stu-id="c7660-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="c7660-198">Výchozí databázi nastavíte tak, že vyberete možnost z rozevíracího seznamu, např.:</span><span class="sxs-lookup"><span data-stu-id="c7660-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="c7660-199">Potom klikněte na kartu přístup k databázi:</span><span class="sxs-lookup"><span data-stu-id="c7660-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="c7660-200">Pro každou databázi, ke které chcete povolit přístup, klikněte na zaškrtávací políčko Povolit.</span><span class="sxs-lookup"><span data-stu-id="c7660-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="c7660-201">Budete také muset vybrat databázové role, zkontrolovat\_DB, že vaše přihlášení bude mít všechna potřebná oprávnění ke správě a používání vybrané databáze.</span><span class="sxs-lookup"><span data-stu-id="c7660-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="c7660-202">Kliknutím na tlačítko OK zavřete dialogové okno Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="c7660-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="c7660-203">Vaše aplikace ASP.NET je teď nakonfigurovaná tak, aby podporovala integrované ověřování SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c7660-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="c7660-204">Nespouštějte ASP.NET 1,0 v nativním režimu IIS 6,0</span><span class="sxs-lookup"><span data-stu-id="c7660-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="c7660-205">ASP.NET 1,0 ve službě IIS 6,0 je podporováno pouze v režimu kompatibility služby IIS 5.</span><span class="sxs-lookup"><span data-stu-id="c7660-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="c7660-206">Pokud chcete nakonfigurovat ASP.NET 1,0 v režimu kompatibility IIS 5,0, otevřete Správce služeb internetu a klikněte pravým tlačítkem na weby a vyberte vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="c7660-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="c7660-207">Chcete přejít na kartu služby a ověřit? Spustit webovou službu v izolovaném režimu služby IIS 5,0?:</span><span class="sxs-lookup"><span data-stu-id="c7660-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
