---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET odepřel přístup k adresářům služby IIS | Microsoft Docs
author: rick-anderson
description: Tento dokument white paper popisuje, co je třeba udělat, pokud požadavek na vaši aplikaci ASP.NET vrátí chybu, "odepřený přístup k adresáři adresáře. Nepovedlo se s...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638500"
---
# <a name="aspnet-denied-access-to-iis-directories"></a><span data-ttu-id="a26f7-104">Aplikace ASP.NET zamítla přístup k adresářům služby IIS</span><span class="sxs-lookup"><span data-stu-id="a26f7-104">ASP.NET Denied Access to IIS Directories</span></span>

> <span data-ttu-id="a26f7-105">Tento dokument white paper popisuje, co je třeba udělat, pokud požadavek na vaši aplikaci ASP.NET vrátí chybu, "odepřený přístup k adresáři *adresáře* .</span><span class="sxs-lookup"><span data-stu-id="a26f7-105">This whitepaper describes what you must do if a request to your ASP.NET application returns the error, "Denied Access to *DirectoryName* directory.</span></span> <span data-ttu-id="a26f7-106">Nepovedlo se spustit monitorování změn adresáře.</span><span class="sxs-lookup"><span data-stu-id="a26f7-106">Failed to start monitoring directory changes."</span></span>
> 
> <span data-ttu-id="a26f7-107">Platí pro ASP.NET 1,0 a ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="a26f7-107">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="a26f7-108">ASP.NET v1 RTM teď používá méně privilegovaný účet systému Windows, který je zaregistrován jako účet ASPNET na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="a26f7-108">ASP.NET V1 RTM now runs using a less privileged windows account - registered as the "ASPNET" account on a local machine.</span></span>

<span data-ttu-id="a26f7-109">V některých uzamčených systémech nemusí tento účet ve výchozím nastavení mít přístup pro čtení k adresářům obsahu webu, kořenovému adresáři aplikace nebo kořenovému adresáři webu.</span><span class="sxs-lookup"><span data-stu-id="a26f7-109">On some locked down systems, this account may not by default have read security access to a website's content directories, the application root directory, or the web site root directory.</span></span> <span data-ttu-id="a26f7-110">V takovém případě se při žádosti o stránky z dané webové aplikace zobrazí následující chyba:</span><span class="sxs-lookup"><span data-stu-id="a26f7-110">In this case you will receive the following error when requesting pages from a given web application:</span></span>

![](denied-access-to-iis-directories/_static/image1.jpg)

<span data-ttu-id="a26f7-111">Chcete-li tento problém vyřešit, budete muset změnit oprávnění zabezpečení pro příslušné adresáře.</span><span class="sxs-lookup"><span data-stu-id="a26f7-111">To fix this you will need to change the security permissions on the appropriate directories.</span></span>

<span data-ttu-id="a26f7-112">Konkrétně ASP.NET vyžaduje přístup pro čtení, spouštění a výpis pro účet ASPNET pro kořen webu (například c:\Inetpub\Wwwroot nebo libovolný alternativní adresář webu, který jste mohli nakonfigurovat ve službě IIS), adresář obsahu a kořenový adresář aplikace. aby bylo možné monitorovat změny konfiguračního souboru.</span><span class="sxs-lookup"><span data-stu-id="a26f7-112">Specifically, ASP.NET requires read, execute, and list access for the ASPNET account for the web site root (for example: c:\inetpub\wwwroot or any alternative site directory you may have configured in IIS), the content directory and the application root directory in order to monitor for configuration file changes.</span></span> <span data-ttu-id="a26f7-113">Kořen aplikace odpovídá cestě ke složce přidružené k virtuálnímu adresáři aplikace v nástroji pro správu služby IIS (inetmgr).</span><span class="sxs-lookup"><span data-stu-id="a26f7-113">The application root corresponds to the folder path associated with the application virtual directory in the IIS Administration tool (inetmgr).</span></span>

<span data-ttu-id="a26f7-114">Podívejte se například na následující hierarchii aplikací ve složce Wwwroot.</span><span class="sxs-lookup"><span data-stu-id="a26f7-114">For example, consider the following application hierarchy under the wwwroot folder.</span></span>

`C:\inetpub\wwwroot\myapp\default.aspx`

<span data-ttu-id="a26f7-115">V tomto příkladu účet ASPNET potřebuje oprávnění ke čtení definovaná výše pro obsah v adresáři MyApp i Wwwroot.</span><span class="sxs-lookup"><span data-stu-id="a26f7-115">For this example, the ASPNET account needs the read permissions defined above for content in both the myapp and the wwwroot directory.</span></span> <span data-ttu-id="a26f7-116">Jeden zděděný seznam řízení přístupu (ACL) kořenové složky se dá volitelně použít i pro oba adresáře, pokud jsou vnořené.</span><span class="sxs-lookup"><span data-stu-id="a26f7-116">A single inherited ACL on the root folder can also be optionally used for both directories if they're nested.</span></span>

<span data-ttu-id="a26f7-117">Chcete-li přidat oprávnění k adresáři, proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="a26f7-117">To add permissions to a directory, perform the following steps:</span></span>

- <span data-ttu-id="a26f7-118">Pomocí Průzkumníka Windows přejděte do adresáře.</span><span class="sxs-lookup"><span data-stu-id="a26f7-118">Using the Windows explorer, navigate to the directory</span></span>
- <span data-ttu-id="a26f7-119">Klikněte pravým tlačítkem na složku adresáře a vyberte vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="a26f7-119">Right click on the directory folder and choose "Properties"</span></span>
- <span data-ttu-id="a26f7-120">Přejděte na kartu zabezpečení v dialogovém okně Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="a26f7-120">Navigate to the "Security" tab on the property dialog</span></span>
- <span data-ttu-id="a26f7-121">Klikněte na tlačítko Přidat a zadejte název počítače následovaný názvem účtu ASPNET.</span><span class="sxs-lookup"><span data-stu-id="a26f7-121">Click the "Add" button and enter the machine name followed by the ASPNET account name.</span></span> <span data-ttu-id="a26f7-122">Například v počítači s názvem "webdev" zadáte webdev\ASPNET a získáte "OK".</span><span class="sxs-lookup"><span data-stu-id="a26f7-122">For example, on a machine named "webdev", you would enter webdev\ASPNET and hit "OK".</span></span>
- <span data-ttu-id="a26f7-123">Ujistěte se, že má účet ASPNET zaškrtnuté políčko číst &amp; spustit, zobrazovat obsah složky a číst.</span><span class="sxs-lookup"><span data-stu-id="a26f7-123">Ensure that the ASPNET account has the "Read &amp; Execute", "List Folder Contents", and "Read" checkboxes checked.</span></span>
- <span data-ttu-id="a26f7-124">Kliknutím na OK zavřete dialogové okno a změny uložte.</span><span class="sxs-lookup"><span data-stu-id="a26f7-124">Hit OK to dismiss the dialog and save the changes.</span></span>

![](denied-access-to-iis-directories/_static/image2.jpg)

<span data-ttu-id="a26f7-125">V případě potřeby je možné tyto změny automatizovat pomocí skriptů nebo nástroje Cacls. exe, který se dodává se systémem Windows.</span><span class="sxs-lookup"><span data-stu-id="a26f7-125">If desired, these changes can be automated using scripts or the "cacls.exe" tool that ships with Windows.</span></span> <span data-ttu-id="a26f7-126">Další informace o účtu ASPNET najdete v [dokumentu nejčastějších dotazů](https://go.microsoft.com/fwlink/?LinkId=5828).</span><span class="sxs-lookup"><span data-stu-id="a26f7-126">For more information on the ASPNET account, please see the [FAQ document](https://go.microsoft.com/fwlink/?LinkId=5828).</span></span>

<span data-ttu-id="a26f7-127">Pokud daná webová aplikace spoléhá na konkrétní složku nebo soubor oprávnění pro zápis nebo změnu, může to být uděleno stejným postupem a zaškrtnutím políček "zapsat" nebo "Upravit".</span><span class="sxs-lookup"><span data-stu-id="a26f7-127">If a given web application relies on having write or modify permissions to a particular folder or file, this can be granted by following the same procedure and checking the "Write" and/or "Modify" checkboxes.</span></span>

<span data-ttu-id="a26f7-128">V počítačích, které povolují všem uživatelům nebo skupinám přístup pro čtení k těmto adresářům (což je výchozí konfigurace), nebudou zjištěny žádné problémy a výše uvedené kroky nebudou nutné.</span><span class="sxs-lookup"><span data-stu-id="a26f7-128">On machines that allow Everyone or the Users group read access to these directories (which is the default configuration), no issues will be encountered and the above steps will not be required.</span></span>
