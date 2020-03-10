---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Volání webového rozhraní API z aplikace Windows Phone 8 (C#)-ASP.NET 4. x
author: rmcmurray
description: 'Kurz s kódem: Vytvoření aplikace webového rozhraní API v ASP.NET v ASP.NET 4. x, která poskytuje katalog knih pro aplikaci Windows Phone 8.'
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614735"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="d4ee2-103">Volání webového rozhraní API z aplikace pro Windows Phone 8 (C#)</span><span class="sxs-lookup"><span data-stu-id="d4ee2-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>

<span data-ttu-id="d4ee2-104">od [Robert blog](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="d4ee2-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="d4ee2-105">V tomto kurzu se naučíte, jak vytvořit úplný kompletní scénář skládající se z aplikace ASP.NET Web API, která poskytuje katalog knih pro aplikaci Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="d4ee2-106">Přehled</span><span class="sxs-lookup"><span data-stu-id="d4ee2-106">Overview</span></span>

<span data-ttu-id="d4ee2-107">Služby RESTful, jako je ASP.NET webové rozhraní API, zjednodušují vytváření aplikací založených na protokolu HTTP pro vývojáře abstrakcí architektury pro aplikace na straně serveru a na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="d4ee2-108">Namísto vytváření proprietárního protokolu založeného na soketu pro komunikaci, vývojáři webového rozhraní API jednoduše potřebují publikovat požadavky HTTP pro svou aplikaci (například: GET, POST, PUT, DELETE) a klientské aplikace jenom potřebují spotřebovat. metody HTTP, které jsou nezbytné pro jejich aplikaci.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="d4ee2-109">V tomto uceleném kurzu se naučíte, jak pomocí webového rozhraní API vytvořit následující projekty:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="d4ee2-110">V [první části tohoto kurzu](#STEP1)vytvoříte aplikaci webového rozhraní API ASP.NET, která bude podporovat všechny operace vytvoření, čtení, aktualizace a odstranění (CRUD) pro správu katalogu knih.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="d4ee2-111">Tato aplikace použije [ukázkový soubor XML (Books. XML)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) z MSDN.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="d4ee2-112">V [druhé části tohoto kurzu](#STEP2)vytvoříte interaktivní aplikaci Windows Phone 8, která načte data z vaší aplikace webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="d4ee2-113">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="d4ee2-113">Prerequisites</span></span>

- <span data-ttu-id="d4ee2-114">Visual Studio 2013 s nainstalovanou sadou Windows Phone 8 SDK</span><span class="sxs-lookup"><span data-stu-id="d4ee2-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="d4ee2-115">Windows 8 nebo novější v 64 systému s nainstalovanou technologií Hyper-V</span><span class="sxs-lookup"><span data-stu-id="d4ee2-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="d4ee2-116">Seznam dalších požadavků najdete v části *požadavky na systém* na stránce pro stažení [sady Windows Phone SDK 8,0](https://www.microsoft.com/download/details.aspx?id=35471) .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="d4ee2-117">Pokud budete testovat připojení mezi webovým rozhraním API a Windows Phone 8 projektů v místním systému, budete muset postupovat podle pokynů v článku *[připojení emulátoru Windows Phone 8 k webovým aplikacím API v místním počítači](https://go.microsoft.com/fwlink/?LinkId=324014)* a nastavení testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="d4ee2-118">Krok 1: vytvoření projektu Bookstore webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="d4ee2-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="d4ee2-119">Prvním krokem tohoto uceleného kurzu je vytvoření projektu webového rozhraní API, který podporuje všechny operace CRUD. Všimněte si, že do tohoto řešení přidáte projekt Windows Phone aplikace v [kroku 2](#STEP2) tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="d4ee2-120">Otevřete **Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="d4ee2-121">Klikněte na **soubor**, **Nový**a pak na **projekt**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="d4ee2-122">Po zobrazení dialogového okna **Nový projekt** rozbalte položku **nainstalováno**, potom **šablony**, **C#vizuál**a pak možnost **Web**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="d4ee2-123">Rozbalte kliknutím na obrázek.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-123">Click image to expand</span></span>                                                                |

4. <span data-ttu-id="d4ee2-124">Zvýrazněte **ASP.NET webová aplikace**, jako název projektu zadejte **Bookstore** a pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="d4ee2-125">Po zobrazení dialogového okna **Nový projekt ASP.NET** vyberte šablonu **webové rozhraní API** a pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="d4ee2-126">Rozbalte kliknutím na obrázek.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-126">Click image to expand</span></span>                                                                |

6. <span data-ttu-id="d4ee2-127">Po otevření projektu webového rozhraní API odeberte z projektu ukázkový kontroler:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="d4ee2-128">Rozbalte složku **Controllers** v Průzkumníkovi řešení.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="d4ee2-129">Klikněte pravým tlačítkem na soubor **ValuesController.cs** a pak klikněte na **Odstranit**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="d4ee2-130">Po zobrazení výzvy k potvrzení odstranění klikněte na **OK** .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="d4ee2-131">Přidejte datový soubor XML do projektu webového rozhraní API; Tento soubor obsahuje obsah katalogu Bookstore:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="d4ee2-132">V Průzkumníku řešení klikněte pravým tlačítkem na složku **aplikace\_data** a pak klikněte na **Přidat**a pak klikněte na **Nová položka**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="d4ee2-133">Jakmile se zobrazí dialogové okno **Přidat novou položku** , zvýrazněte šablonu **souboru XML** .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="d4ee2-134">Pojmenujte soubor **Books. XML**a potom klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="d4ee2-135">Po otevření souboru **Books. XML** nahraďte kód v souboru souborem XML z ukázkových **knih. XML** na webu MSDN:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="d4ee2-136">Uložte a zavřete soubor XML.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="d4ee2-137">Přidejte model Bookstore do projektu webového rozhraní API; Tento model obsahuje logiku vytváření, čtení, aktualizace a odstranění (CRUD) pro aplikaci Bookstore:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="d4ee2-138">V Průzkumníku řešení klikněte pravým tlačítkem na složku **modely** , potom klikněte na **Přidat**a potom klikněte na **Třída**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="d4ee2-139">Když se zobrazí dialogové okno **Přidat novou položku** , pojmenujte soubor třídy **BookDetails.cs**a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="d4ee2-140">Po otevření souboru **BookDetails.cs** nahraďte kód v souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="d4ee2-141">Uložte a zavřete soubor **BookDetails.cs** .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="d4ee2-142">Přidejte kontroler Bookstore do projektu webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="d4ee2-143">V Průzkumníku řešení klikněte pravým tlačítkem na složku **řadiče** a pak klikněte na **Přidat**a potom na **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="d4ee2-144">Po zobrazení dialogového okna **Přidat generování uživatelského rozhraní** zvýrazněte možnost **KONTROLER webového rozhraní API 2 – prázdné**a pak klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="d4ee2-145">Po zobrazení dialogového okna **Přidat řadič** pojmenujte kontrolér **BooksController**a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="d4ee2-146">Po otevření souboru **BooksController.cs** nahraďte kód v souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="d4ee2-147">Uložte a zavřete soubor **BooksController.cs** .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="d4ee2-148">Sestavte aplikaci webového rozhraní API, aby kontrolovala chyby.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="d4ee2-149">Krok 2: Přidání projektu katalogu Bookstore pro Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="d4ee2-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="d4ee2-150">Dalším krokem tohoto kompletního scénáře je vytvoření aplikace katalogu pro Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="d4ee2-151">Tato aplikace bude používat šablonu *aplikace Windows Phone Data Bound* pro výchozí uživatelské rozhraní a bude používat aplikaci webového rozhraní API, kterou jste vytvořili v [kroku 1](#STEP1) tohoto kurzu jako zdroj dat.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="d4ee2-152">V Průzkumníku řešení klikněte pravým tlačítkem na řešení **Bookstore** a pak klikněte na **Přidat**a **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="d4ee2-153">Po zobrazení dialogového okna **Nový projekt** rozbalte položku **nainstalováno**, **C#vizuál**a poté **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="d4ee2-154">Zvýrazněte **Windows Phone aplikace datové vazby**, jako název zadejte **BookCatalog** a pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="d4ee2-155">Přidejte do projektu **BookCatalog** balíček NuGet JSON.NET:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="d4ee2-156">V Průzkumníku řešení klikněte pravým tlačítkem na **odkazy** pro projekt **BookCatalog** a pak klikněte na **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="d4ee2-157">Po zobrazení dialogového okna **Spravovat balíčky NuGet** rozbalte oddíl **Online** a zvýrazněte **NuGet.org**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="d4ee2-158">Do vyhledávacího pole zadejte **JSON.NET** a klikněte na ikonu hledání.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="d4ee2-159">Ve výsledcích hledání zvýrazněte **JSON.NET** a pak klikněte na **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="d4ee2-160">Po dokončení instalace klikněte na **Zavřít**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="d4ee2-161">Přidejte model **BookDetails** do projektu **BookCatalog** ; obsahuje obecný model třídy Bookstore:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="d4ee2-162">V Průzkumníku řešení klikněte pravým tlačítkem na projekt **BookCatalog** , pak klikněte na **Přidat**a potom na **Nová složka**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="d4ee2-163">Pojmenujte nové **modely**složek.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="d4ee2-164">V Průzkumníku řešení klikněte pravým tlačítkem na složku **modely** , potom klikněte na **Přidat**a potom klikněte na **Třída**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="d4ee2-165">Když se zobrazí dialogové okno **Přidat novou položku** , pojmenujte soubor třídy **BookDetails.cs**a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="d4ee2-166">Po otevření souboru **BookDetails.cs** nahraďte kód v souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="d4ee2-167">Uložte a zavřete soubor **BookDetails.cs** .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="d4ee2-168">Aktualizujte třídu **MainViewModel.cs** tak, aby zahrnovala funkce pro komunikaci s aplikací webového rozhraní API pro Bookstore:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="d4ee2-169">Rozbalte složku **ViewModels** v Průzkumníku řešení a dvakrát klikněte na soubor **MainViewModel.cs** .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="d4ee2-170">Po otevření souboru **MainViewModel.cs** nahraďte kód v souboru následujícím kódem: Všimněte si, že budete muset aktualizovat hodnotu `apiUrl` konstanty se skutečnou adresou URL webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="d4ee2-171">Uložte a zavřete soubor **MainViewModel.cs** .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="d4ee2-172">Chcete-li přizpůsobit název aplikace, aktualizujte soubor **MainPage. XAML** :</span><span class="sxs-lookup"><span data-stu-id="d4ee2-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="d4ee2-173">Dvakrát klikněte na soubor **MainPage. XAML** v Průzkumníkovi řešení.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="d4ee2-174">Po otevření souboru **MainPage. XAML** vyhledejte následující řádky kódu:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="d4ee2-175">Nahraďte tyto řádky následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="d4ee2-176">Uložte a zavřete soubor **MainPage. XAML** .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="d4ee2-177">Chcete-li upravit zobrazené položky, aktualizujte soubor **DetailsPage. XAML** :</span><span class="sxs-lookup"><span data-stu-id="d4ee2-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="d4ee2-178">Dvakrát klikněte na soubor **DetailsPage. XAML** v Průzkumníkovi řešení.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="d4ee2-179">Po otevření souboru **DetailsPage. XAML** vyhledejte následující řádky kódu:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="d4ee2-180">Nahraďte tyto řádky následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="d4ee2-181">Uložte a zavřete soubor **DetailsPage. XAML** .</span><span class="sxs-lookup"><span data-stu-id="d4ee2-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="d4ee2-182">Sestavte aplikaci Windows Phone pro kontrolu chyb.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="d4ee2-183">Krok 3: testování kompletního řešení</span><span class="sxs-lookup"><span data-stu-id="d4ee2-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="d4ee2-184">Jak je uvedeno v části *požadavky* v tomto kurzu, když testujete připojení mezi WEBOVÝm rozhraním api a Windows Phone 8 projektů v místním systému, budete muset postupovat podle pokynů v článku *[připojení emulátoru Windows Phone 8 k webovým aplikacím API v místním počítači](https://go.microsoft.com/fwlink/?LinkId=324014)* , abyste mohli nastavit testovací prostředí.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="d4ee2-185">Po nakonfigurování testovacího prostředí budete muset nastavit aplikaci Windows Phone jako spouštěný projekt.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="d4ee2-186">Provedete to tak, že v Průzkumníku řešení zvýrazníte aplikaci **BookCatalog** a pak kliknete na **nastavit jako spouštěný projekt**:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="d4ee2-187">Rozbalte kliknutím na obrázek.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-187">Click image to expand</span></span> |

<span data-ttu-id="d4ee2-188">Když stisknete klávesu F5, Visual Studio spustí emulátor Windows Phone, který zobrazí &quot;při načítání dat aplikace z webového rozhraní API počkat&quot; zprávu:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="d4ee2-189">Rozbalte kliknutím na obrázek.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-189">Click image to expand</span></span> |

<span data-ttu-id="d4ee2-190">Pokud je všechno úspěšné, měli byste vidět zobrazený katalog:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="d4ee2-191">Rozbalte kliknutím na obrázek.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-191">Click image to expand</span></span> |

<span data-ttu-id="d4ee2-192">Pokud klepnete na název knihy, aplikace zobrazí popis knihy:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="d4ee2-193">Rozbalte kliknutím na obrázek.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-193">Click image to expand</span></span> |

<span data-ttu-id="d4ee2-194">Pokud aplikace nemůže komunikovat s webovým rozhraním API, zobrazí se chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="d4ee2-195">Rozbalte kliknutím na obrázek.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-195">Click image to expand</span></span> |

<span data-ttu-id="d4ee2-196">Pokud klepnete na chybovou zprávu, zobrazí se další podrobnosti o této chybě:</span><span class="sxs-lookup"><span data-stu-id="d4ee2-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="d4ee2-197">Rozbalte kliknutím na obrázek.</span><span class="sxs-lookup"><span data-stu-id="d4ee2-197">Click image to expand</span></span>                                                                 |
