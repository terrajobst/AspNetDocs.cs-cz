---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: Upgrade aplikace ASP.NET MVC 1,0 na ASP.NET MVC 2 | Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje, jak ručně upgradovat a pomocí Průvodce aplikaci ASP.NET MVC 1,0 na ASP.NET MVC 2. Tento dokument je také k dispozici pro d...
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637016"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a><span data-ttu-id="e482d-104">Upgrade aplikace ASP.NET MVC 1.0 na ASP.NET MVC 2</span><span class="sxs-lookup"><span data-stu-id="e482d-104">Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2</span></span>

> <span data-ttu-id="e482d-105">Tento dokument popisuje, jak ručně upgradovat a pomocí Průvodce aplikaci ASP.NET MVC 1,0 na ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="e482d-105">This document describes both how to upgrade manually and with a wizard an ASP.NET MVC 1.0 Application to ASP.NET MVC 2.</span></span> <span data-ttu-id="e482d-106">Tento dokument je také k dispozici ke [stažení](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf) .</span><span class="sxs-lookup"><span data-stu-id="e482d-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span></span>

## <a name="introduction"></a><span data-ttu-id="e482d-107">Úvod</span><span class="sxs-lookup"><span data-stu-id="e482d-107">Introduction</span></span>

<span data-ttu-id="e482d-108">ASP.NET MVC 2 se dá nainstalovat vedle sebe s ASP.NET MVC 1,0 na stejném serveru.</span><span class="sxs-lookup"><span data-stu-id="e482d-108">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server.</span></span> <span data-ttu-id="e482d-109">To dává vývojářům aplikací flexibilitu při rozhodování o upgradu aplikace ASP.NET MVC 1,0 na ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="e482d-109">This gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span>

<span data-ttu-id="e482d-110">Visual Studio 2010 obsahuje průvodce, který upgraduje stávající projekty ASP.NET MVC 1,0 vytvořené pomocí sady Visual Studio 2008 na ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="e482d-110">Visual Studio 2010 includes a wizard that upgrades existing ASP.NET MVC 1.0 projects built with Visual Studio 2008 to ASP.NET MVC 2.</span></span> <span data-ttu-id="e482d-111">Průvodce upgradem se spouští otevřením projektu ASP.NET MVC 1,0 v aplikaci Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="e482d-111">The upgrade wizard is initiated by opening an ASP.NET MVC 1.0 project in Visual Studio 2010.</span></span>

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a><span data-ttu-id="e482d-112">Průvodce upgradem pro ASP.NET MVC 1,0 ve Visual Studiu 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="e482d-112">Upgrade Wizard for ASP.NET MVC 1.0 on Visual Studio 2008 SP1</span></span>

<span data-ttu-id="e482d-113">K upgradu aplikace ASP.NET MVC 1,0 na ASP.NET MVC 2 v aplikaci Visual Studio 2008 SP1 použijte MvcAppConverter aplikaci (nepodporované).</span><span class="sxs-lookup"><span data-stu-id="e482d-113">To upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2 in Visual Studio 2008 SP1, use the (unsupported) MvcAppConverter application.</span></span> <span data-ttu-id="e482d-114">Tuto aplikaci si můžete stáhnout z následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="e482d-114">You can download this application from the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a><span data-ttu-id="e482d-115">Ruční upgrade projektu ASP.NET MVC 1,0</span><span class="sxs-lookup"><span data-stu-id="e482d-115">Manually Upgrading an ASP.NET MVC 1.0 Project</span></span>

<span data-ttu-id="e482d-116">Pokud chcete ručně upgradovat existující aplikaci ASP.NET MVC 1,0 na verzi 2, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="e482d-116">To manually upgrade an existing ASP.NET MVC 1.0 application to version 2, follow these steps:</span></span>

1. <span data-ttu-id="e482d-117">Vytvořte zálohu existujícího projektu.</span><span class="sxs-lookup"><span data-stu-id="e482d-117">Make a backup of the existing project.</span></span>
2. <span data-ttu-id="e482d-118">V textovém editoru otevřete soubor projektu (soubor s příponou souboru. csproj nebo. vbproj) a vyhledejte element ProjectTypeGuid.</span><span class="sxs-lookup"><span data-stu-id="e482d-118">In a text editor, open the project file (the file with the .csproj or .vbproj file extension) and find the ProjectTypeGuid element.</span></span> <span data-ttu-id="e482d-119">Jako hodnotu tohoto elementu nahraďte GUID {603c0e0b-db56-11dc-be95-000d561079b0} hodnotou {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span><span class="sxs-lookup"><span data-stu-id="e482d-119">As the value of that element, replace the GUID {603c0e0b-db56-11dc-be95-000d561079b0} with {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span></span> <span data-ttu-id="e482d-120">Až budete hotovi, hodnota tohoto prvku by měla být následující:</span><span class="sxs-lookup"><span data-stu-id="e482d-120">When you are done, the value of that element should be as follows:</span></span> 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. <span data-ttu-id="e482d-121">V kořenové složce webové aplikace upravte soubor Web. config.</span><span class="sxs-lookup"><span data-stu-id="e482d-121">In the Web application root folder, edit the Web.config file.</span></span> <span data-ttu-id="e482d-122">Vyhledejte System. Web. Mvc, Version = 1.0.0.0 a nahraďte všechny instance pomocí System. Web. Mvc, Version = 2.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="e482d-122">Search for System.Web.Mvc, Version=1.0.0.0 and replace all instances with System.Web.Mvc, Version=2.0.0.0.</span></span>
4. <span data-ttu-id="e482d-123">Opakujte předchozí krok pro soubor Web. config umístěný ve složce views.</span><span class="sxs-lookup"><span data-stu-id="e482d-123">Repeat the previous step for the Web.config file located in the Views folder.</span></span>
5. <span data-ttu-id="e482d-124">Otevřete projekt pomocí sady Visual Studio a v **Průzkumník řešení**rozbalte uzel **odkazy** .</span><span class="sxs-lookup"><span data-stu-id="e482d-124">Open the project using Visual Studio, and in **Solution Explorer**, expand the **References** node.</span></span> <span data-ttu-id="e482d-125">Odstraňte odkaz na System. Web. Mvc (který odkazuje na sestavení verze 1,0).</span><span class="sxs-lookup"><span data-stu-id="e482d-125">Delete the reference to System.Web.Mvc (which points to the version 1.0 assembly).</span></span> <span data-ttu-id="e482d-126">Přidejte odkaz na System. Web. Mvc (v 2.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="e482d-126">Add a reference to System.Web.Mvc (v2.0.0.0).</span></span>
6. <span data-ttu-id="e482d-127">Přidejte následující element bindingRedirect do souboru Web. config v kořenovém adresáři aplikace v části zobrazí dostupných:</span><span class="sxs-lookup"><span data-stu-id="e482d-127">Add the following bindingRedirect element to the Web.config file in the application root under the configuraton section:</span></span>   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. <span data-ttu-id="e482d-128">Vytvořte novou prázdnou aplikaci ASP.NET MVC 2.</span><span class="sxs-lookup"><span data-stu-id="e482d-128">Create a new empty ASP.NET MVC 2 application.</span></span> <span data-ttu-id="e482d-129">Zkopírujte soubory ze složky skripty nové aplikace do složky skripty v existující aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e482d-129">Copy the files from the Scripts folder of the new application into the Scripts folder of the existing application.</span></span>
8. <span data-ttu-id="e482d-130">Aktualizujte existující soubor aplikace. €™ s CSS definicemi stylů CSS v souboru Web. CSS.</span><span class="sxs-lookup"><span data-stu-id="e482d-130">Update the existing applicationâ€™s CSS file with the CSS style definitions in the Site.css file.</span></span>
9. <span data-ttu-id="e482d-131">Zkompilujte aplikaci a spusťte ji.</span><span class="sxs-lookup"><span data-stu-id="e482d-131">Compile the application and run it.</span></span> <span data-ttu-id="e482d-132">Pokud dojde k nějakým chybám, přečtěte si část důležité změny na stránce [co je nového v ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) .</span><span class="sxs-lookup"><span data-stu-id="e482d-132">If any errors occur, refer to the Breaking Changes section of the [What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) page.</span></span>
