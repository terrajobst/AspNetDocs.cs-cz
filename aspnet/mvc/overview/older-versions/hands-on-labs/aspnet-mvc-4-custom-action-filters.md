---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: Filtry vlastních akcí ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC poskytuje filtry akcí pro zpracování logiky filtrování před nebo po volání metody Action. Filtry akcí jsou vlastní atributy Tha...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579693"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a><span data-ttu-id="b6200-104">ASP.NET MVC 4 – filtr vlastních akcí</span><span class="sxs-lookup"><span data-stu-id="b6200-104">ASP.NET MVC 4 Custom Action Filters</span></span>

<span data-ttu-id="b6200-105">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="b6200-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="b6200-106">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="b6200-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="b6200-107">ASP.NET MVC poskytuje filtry akcí pro zpracování logiky filtrování před nebo po volání metody Action.</span><span class="sxs-lookup"><span data-stu-id="b6200-107">ASP.NET MVC provides Action Filters for executing filtering logic either before or after an action method is called.</span></span> <span data-ttu-id="b6200-108">Filtry akcí jsou vlastní atributy, které poskytují deklarativní způsob, jak přidat chování před akcemi a následnou akcím do metod akcí kontroleru.</span><span class="sxs-lookup"><span data-stu-id="b6200-108">Action Filters are custom attributes that provide declarative means to add pre-action and post-action behavior to the controller's action methods.</span></span>

<span data-ttu-id="b6200-109">V tomto praktickém testovacím prostředí vytvoříte vlastní atribut action Filter do řešení MvcMusicStore pro zachycení požadavků kontroléru a Zaprotokolujte aktivitu lokality do databázové tabulky.</span><span class="sxs-lookup"><span data-stu-id="b6200-109">In this Hands-on Lab you will create a custom action filter attribute into MvcMusicStore solution to catch controller's requests and log the activity of a site into a database table.</span></span> <span data-ttu-id="b6200-110">Filtr protokolování budete moct přidat vložením do libovolného kontroleru nebo akce.</span><span class="sxs-lookup"><span data-stu-id="b6200-110">You will be able to add your logging filter by injection to any controller or action.</span></span> <span data-ttu-id="b6200-111">Nakonec se zobrazí zobrazení protokolu, které zobrazuje seznam návštěvníků.</span><span class="sxs-lookup"><span data-stu-id="b6200-111">Finally, you will see the log view that shows the list of visitors.</span></span>

<span data-ttu-id="b6200-112">Tato praktická cvičení předpokládá, že máte základní znalosti o **ASP.NET MVC**.</span><span class="sxs-lookup"><span data-stu-id="b6200-112">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="b6200-113">Pokud jste ještě **ASP.NET MVC** nepoužívali, doporučujeme, abyste si převzali v praxi **ASP.NET MVC 4** pro praktické cvičení.</span><span class="sxs-lookup"><span data-stu-id="b6200-113">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="b6200-114">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Training Kit, která je dostupná v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="b6200-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="b6200-115">Projekt, který je specifický pro toto testovací prostředí, je k dispozici ve [vlastních filtrech akcí ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span><span class="sxs-lookup"><span data-stu-id="b6200-115">The project specific to this lab is available at [ASP.NET MVC 4 Custom Action Filters](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="b6200-116">Cíle</span><span class="sxs-lookup"><span data-stu-id="b6200-116">Objectives</span></span>

<span data-ttu-id="b6200-117">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="b6200-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="b6200-118">Vytvoření vlastního atributu filtru akcí pro rozšiřování možností filtrování</span><span class="sxs-lookup"><span data-stu-id="b6200-118">Create a custom action filter attribute to extend filtering capabilities</span></span>
- <span data-ttu-id="b6200-119">Použití vlastního atributu filtru vložením na určitou úroveň</span><span class="sxs-lookup"><span data-stu-id="b6200-119">Apply a custom filter attribute by injection to a specific level</span></span>
- <span data-ttu-id="b6200-120">Globální registrace filtrů vlastních akcí</span><span class="sxs-lookup"><span data-stu-id="b6200-120">Register a custom action filters globally</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="b6200-121">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="b6200-121">Prerequisites</span></span>

<span data-ttu-id="b6200-122">K dokončení tohoto testovacího prostředí musíte mít následující položky:</span><span class="sxs-lookup"><span data-stu-id="b6200-122">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="b6200-123">[Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).</span><span class="sxs-lookup"><span data-stu-id="b6200-123">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="b6200-124">Nastavení</span><span class="sxs-lookup"><span data-stu-id="b6200-124">Setup</span></span>

<span data-ttu-id="b6200-125">**Instalace fragmentů kódu**</span><span class="sxs-lookup"><span data-stu-id="b6200-125">**Installing Code Snippets**</span></span>

<span data-ttu-id="b6200-126">Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6200-126">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="b6200-127">Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .</span><span class="sxs-lookup"><span data-stu-id="b6200-127">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="b6200-128">Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze C: použití fragmentů kódu](#AppendixC)&quot;.</span><span class="sxs-lookup"><span data-stu-id="b6200-128">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="b6200-129">Cvičení</span><span class="sxs-lookup"><span data-stu-id="b6200-129">Exercises</span></span>

<span data-ttu-id="b6200-130">Tato praktická cvičení se skládají z následujících cvičení:</span><span class="sxs-lookup"><span data-stu-id="b6200-130">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="b6200-131">Cvičení 1: protokolování akcí</span><span class="sxs-lookup"><span data-stu-id="b6200-131">Exercise 1: Logging actions</span></span>](#Exercise1)
2. [<span data-ttu-id="b6200-132">Cvičení 2: Správa více filtrů akcí</span><span class="sxs-lookup"><span data-stu-id="b6200-132">Exercise 2: Managing Multiple Action Filters</span></span>](#Exercise2)

<span data-ttu-id="b6200-133">Odhadovaný čas dokončení tohoto testovacího prostředí: **30 minut**.</span><span class="sxs-lookup"><span data-stu-id="b6200-133">Estimated time to complete this lab: **30 minutes**.</span></span>

> [!NOTE]
> <span data-ttu-id="b6200-134">Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení.</span><span class="sxs-lookup"><span data-stu-id="b6200-134">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="b6200-135">Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.</span><span class="sxs-lookup"><span data-stu-id="b6200-135">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a><span data-ttu-id="b6200-136">Cvičení 1: protokolování akcí</span><span class="sxs-lookup"><span data-stu-id="b6200-136">Exercise 1: Logging Actions</span></span>

<span data-ttu-id="b6200-137">V tomto cvičení se naučíte, jak vytvořit vlastní filtr protokolu akcí pomocí zprostředkovatelů filtru ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="b6200-137">In this exercise, you will learn how to create a custom action log filter by using ASP.NET MVC 4 Filter Providers.</span></span> <span data-ttu-id="b6200-138">Pro tento účel použijete filtr protokolování na web MusicStore, který bude zaznamená všechny aktivity ve vybraných řadičích.</span><span class="sxs-lookup"><span data-stu-id="b6200-138">For that purpose you will apply a logging filter to the MusicStore site that will record all the activities in the selected controllers.</span></span>

<span data-ttu-id="b6200-139">Filtr rozšíří **ActionFilterAttributeClass** a přepíše metodu **OnActionExecuting** pro zachycení jednotlivých požadavků a následné provádění akcí protokolování.</span><span class="sxs-lookup"><span data-stu-id="b6200-139">The filter will extend **ActionFilterAttributeClass** and override **OnActionExecuting** method to catch each request and then perform the logging actions.</span></span> <span data-ttu-id="b6200-140">Kontextové informace o požadavcích HTTP, spouštění metod, výsledků a parametrech budou poskytnuty třídou ASP.NET MVC **ActionExecutingContext** **.**</span><span class="sxs-lookup"><span data-stu-id="b6200-140">The context information about HTTP requests, executing methods, results and parameters will be provided by ASP.NET MVC **ActionExecutingContext** class **.**</span></span>

> [!NOTE]
> <span data-ttu-id="b6200-141">ASP.NET MVC 4 má také výchozí zprostředkovatele filtrů, které můžete použít bez vytvoření vlastního filtru.</span><span class="sxs-lookup"><span data-stu-id="b6200-141">ASP.NET MVC 4 also has default filters providers you can use without creating a custom filter.</span></span> <span data-ttu-id="b6200-142">ASP.NET MVC 4 nabízí následující typy filtrů:</span><span class="sxs-lookup"><span data-stu-id="b6200-142">ASP.NET MVC 4 provides the following types of filters:</span></span>
> 
> - <span data-ttu-id="b6200-143">Filtr **autorizace** , který umožňuje rozhodování o zabezpečení, zda se má provést metoda akce, například provedení ověření nebo ověření vlastností žádosti.</span><span class="sxs-lookup"><span data-stu-id="b6200-143">**Authorization** filter, which makes security decisions about whether to execute an action method, such as performing authentication or validating properties of the request.</span></span>
> - <span data-ttu-id="b6200-144">Filtr **akcí** , který zabalí provádění metody Action.</span><span class="sxs-lookup"><span data-stu-id="b6200-144">**Action** filter, which wraps the action method execution.</span></span> <span data-ttu-id="b6200-145">Tento filtr může provádět další zpracování, například poskytnutí dalších dat metodě akce, kontrolu návratové hodnoty nebo zrušení provádění metody Action.</span><span class="sxs-lookup"><span data-stu-id="b6200-145">This filter can perform additional processing, such as providing extra data to the action method, inspecting the return value, or canceling execution of the action method</span></span>
> - <span data-ttu-id="b6200-146">Filtr **výsledků** , který zabalí provádění objektu ActionResult.</span><span class="sxs-lookup"><span data-stu-id="b6200-146">**Result** filter, which wraps execution of the ActionResult object.</span></span> <span data-ttu-id="b6200-147">Tento filtr může provést další zpracování výsledku, jako je například změna odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="b6200-147">This filter can perform additional processing of the result, such as modifying the HTTP response.</span></span>
> - <span data-ttu-id="b6200-148">Filtr **výjimek** , který se spustí, pokud je v metodě Action vyvolána neošetřená výjimka, počínaje filtry autorizace a končí prováděním výsledku.</span><span class="sxs-lookup"><span data-stu-id="b6200-148">**Exception** filter, which executes if there is an unhandled exception thrown somewhere in action method, starting with the authorization filters and ending with the execution of the result.</span></span> <span data-ttu-id="b6200-149">Filtry výjimek lze použít pro úlohy, jako je protokolování nebo zobrazení chybové stránky.</span><span class="sxs-lookup"><span data-stu-id="b6200-149">Exception filters can be used for tasks such as logging or displaying an error page.</span></span>
> 
> <span data-ttu-id="b6200-150">Další informace o zprostředkovatelích filtrů najdete na tomto odkazu na webu MSDN: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)).</span><span class="sxs-lookup"><span data-stu-id="b6200-150">For more information about Filters Providers please visit this MSDN link: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)) .</span></span>

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a><span data-ttu-id="b6200-151">Informace o funkci protokolování hudby pro aplikace MVC pro Store</span><span class="sxs-lookup"><span data-stu-id="b6200-151">About MVC Music Store Application logging feature</span></span>

<span data-ttu-id="b6200-152">Toto řešení pro hudební úložiště obsahuje novou tabulku datového modelu pro protokolování lokality **ActionLog**s následujícími poli: název řadiče, který obdržel požadavek, se nazývá akce, IP adresa klienta a časové razítko.</span><span class="sxs-lookup"><span data-stu-id="b6200-152">This Music Store solution has a new data model table for site logging, **ActionLog**, with the following fields: Name of the controller that received a request, Called action, Client IP and Time stamp.</span></span>

<span data-ttu-id="b6200-153">![Datový model. Tabulka ActionLog](aspnet-mvc-4-custom-action-filters/_static/image1.png "Datový model. Tabulka ActionLog")</span><span class="sxs-lookup"><span data-stu-id="b6200-153">![Data model. ActionLog table.](aspnet-mvc-4-custom-action-filters/_static/image1.png "Data model. ActionLog table.")</span></span>

<span data-ttu-id="b6200-154">*Datový model – tabulka ActionLog*</span><span class="sxs-lookup"><span data-stu-id="b6200-154">*Data model - ActionLog table*</span></span>

<span data-ttu-id="b6200-155">Řešení poskytuje zobrazení ASP.NET MVC pro protokol akcí, který lze najít v **MvcMusicStores/views/ActionLog**:</span><span class="sxs-lookup"><span data-stu-id="b6200-155">The solution provides an ASP.NET MVC View for the Action log that can be found at **MvcMusicStores/Views/ActionLog**:</span></span>

<span data-ttu-id="b6200-156">![Zobrazení protokolu akcí](aspnet-mvc-4-custom-action-filters/_static/image2.png "Zobrazení protokolu akcí")</span><span class="sxs-lookup"><span data-stu-id="b6200-156">![Action Log view](aspnet-mvc-4-custom-action-filters/_static/image2.png "Action Log view")</span></span>

<span data-ttu-id="b6200-157">*Zobrazení protokolu akcí*</span><span class="sxs-lookup"><span data-stu-id="b6200-157">*Action Log view*</span></span>

<span data-ttu-id="b6200-158">U této struktury se bude všechny práce zaměřit na požadavek řadiče s přerušením a provádění protokolování pomocí vlastního filtrování.</span><span class="sxs-lookup"><span data-stu-id="b6200-158">With this given structure, all the work will be focused on interrupting controller's request and performing the logging by using custom filtering.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a><span data-ttu-id="b6200-159">Úloha 1 – Vytvoření vlastního filtru pro zachycení žádosti řadiče</span><span class="sxs-lookup"><span data-stu-id="b6200-159">Task 1 - Creating a Custom Filter to Catch a Controller's Request</span></span>

<span data-ttu-id="b6200-160">V této úloze vytvoříte vlastní třídu atributů filtru, která bude obsahovat logiku protokolování.</span><span class="sxs-lookup"><span data-stu-id="b6200-160">In this task you will create a custom filter attribute class that will contain the logging logic.</span></span> <span data-ttu-id="b6200-161">Pro tento účel budete rozšířeni třídu ASP.NET MVC **ActionFilterAttribute** a implementujete rozhraní **IActionFilter**.</span><span class="sxs-lookup"><span data-stu-id="b6200-161">For that purpose you will extend ASP.NET MVC **ActionFilterAttribute** Class and implement the interface **IActionFilter**.</span></span>

> [!NOTE]
> <span data-ttu-id="b6200-162">**ActionFilterAttribute** je základní třídou pro všechny filtry atributů.</span><span class="sxs-lookup"><span data-stu-id="b6200-162">The **ActionFilterAttribute** is the base class for all the attribute filters.</span></span> <span data-ttu-id="b6200-163">Poskytuje následující metody pro spuštění konkrétní logiky po a před provedením akce kontroleru:</span><span class="sxs-lookup"><span data-stu-id="b6200-163">It provides the following methods to execute a specific logic after and before controller action's execution:</span></span>
> 
> - <span data-ttu-id="b6200-164">**OnActionExecuting**(ActionExecutingContext filterContext): těsně před voláním metody Action.</span><span class="sxs-lookup"><span data-stu-id="b6200-164">**OnActionExecuting**(ActionExecutingContext filterContext): Just before the action method is called.</span></span>
> - <span data-ttu-id="b6200-165">**OnActionExecuted**(ActionExecutedContext filterContext): po volání metody Action a před provedením výsledku (před zobrazením vykreslování).</span><span class="sxs-lookup"><span data-stu-id="b6200-165">**OnActionExecuted**(ActionExecutedContext filterContext): After the action method is called and before the result is executed (before view render).</span></span>
> - <span data-ttu-id="b6200-166">**OnResultExecuting**(ResultExecutingContext filterContext): těsně před provedením výsledku (před zobrazením vykreslování).</span><span class="sxs-lookup"><span data-stu-id="b6200-166">**OnResultExecuting**(ResultExecutingContext filterContext): Just before the result is executed (before view render).</span></span>
> - <span data-ttu-id="b6200-167">**OnResultExecuted**(ResultExecutedContext filterContext): po provedení výsledku (po vykreslení zobrazení).</span><span class="sxs-lookup"><span data-stu-id="b6200-167">**OnResultExecuted**(ResultExecutedContext filterContext): After the result is executed (after the view is rendered).</span></span>
> 
> <span data-ttu-id="b6200-168">Přepsáním kterékoli z těchto metod na odvozenou třídu můžete spustit vlastní kód pro filtrování.</span><span class="sxs-lookup"><span data-stu-id="b6200-168">By overriding any of these methods into a derived class, you can execute your own filtering code.</span></span>

1. <span data-ttu-id="b6200-169">Otevřete řešení **začít** umístěné ve složce **\Source\Ex01-LoggingActions\Begin** .</span><span class="sxs-lookup"><span data-stu-id="b6200-169">Open the **Begin** solution located at **\Source\Ex01-LoggingActions\Begin** folder.</span></span>

   1. <span data-ttu-id="b6200-170">Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="b6200-170">You will need to download some missing NuGet packages before you continue.</span></span> <span data-ttu-id="b6200-171">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b6200-171">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="b6200-172">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="b6200-172">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="b6200-173">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="b6200-173">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="b6200-174">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="b6200-174">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="b6200-175">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="b6200-175">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="b6200-176">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="b6200-176">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="b6200-177">Další informace najdete v tomto článku: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="b6200-177">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="b6200-178">Přidejte novou C# třídu do složky **Filters** a pojmenujte ji *CustomActionFilter.cs*.</span><span class="sxs-lookup"><span data-stu-id="b6200-178">Add a new C# class into the **Filters** folder and name it *CustomActionFilter.cs*.</span></span> <span data-ttu-id="b6200-179">Tato složka bude ukládat všechny vlastní filtry.</span><span class="sxs-lookup"><span data-stu-id="b6200-179">This folder will store all the custom filters.</span></span>
3. <span data-ttu-id="b6200-180">Otevřete **CustomActionFilter.cs** a přidejte odkaz na obory názvů **System. Web. Mvc** a **MvcMusicStore. Models** :</span><span class="sxs-lookup"><span data-stu-id="b6200-180">Open **CustomActionFilter.cs** and add a reference to **System.Web.Mvc** and **MvcMusicStore.Models** namespaces:</span></span>

    <span data-ttu-id="b6200-181">(Fragment kódu – *ASP.NET MVC 4 – filtry vlastních akcí – EX1-CustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="b6200-181">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-CustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. <span data-ttu-id="b6200-182">Dědí třídu **CustomActionFilter** z **ActionFilterAttribute** a pak třídu **CustomActionFilter** implementují rozhraní **IActionFilter** .</span><span class="sxs-lookup"><span data-stu-id="b6200-182">Inherit the **CustomActionFilter** class from **ActionFilterAttribute** and then make **CustomActionFilter** class implement **IActionFilter** interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. <span data-ttu-id="b6200-183">Udělejte třídu **CustomActionFilter** přepsání metody **OnActionExecuting** a přidejte potřebnou logiku pro protokolování provádění filtru.</span><span class="sxs-lookup"><span data-stu-id="b6200-183">Make **CustomActionFilter** class override the method **OnActionExecuting** and add the necessary logic to log the filter's execution.</span></span> <span data-ttu-id="b6200-184">K tomu přidejte následující zvýrazněný kód v rámci třídy **CustomActionFilter** .</span><span class="sxs-lookup"><span data-stu-id="b6200-184">To do this, add the following highlighted code within **CustomActionFilter** class.</span></span>

    <span data-ttu-id="b6200-185">(Fragment kódu – *ASP.NET MVC 4 – filtry vlastních akcí – EX1-LoggingActions*)</span><span class="sxs-lookup"><span data-stu-id="b6200-185">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex1-LoggingActions*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > <span data-ttu-id="b6200-186">Metoda **OnActionExecuting** používá **Entity Framework** k přidání nového registru ActionLog.</span><span class="sxs-lookup"><span data-stu-id="b6200-186">**OnActionExecuting** method is using **Entity Framework** to add a new ActionLog register.</span></span> <span data-ttu-id="b6200-187">Vytvoří a vyplní novou instanci entity s informacemi o kontextu z **filterContext**.</span><span class="sxs-lookup"><span data-stu-id="b6200-187">It creates and fills a new entity instance with the context information from **filterContext**.</span></span>
    > 
    > <span data-ttu-id="b6200-188">Další informace o třídě **ControllerContext** najdete na [webu MSDN](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6200-188">You can read more about **ControllerContext** class at [msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a><span data-ttu-id="b6200-189">Úloha 2 – vložení Zachytávosti kódu do třídy kontroleru úložiště</span><span class="sxs-lookup"><span data-stu-id="b6200-189">Task 2 - Injecting a Code Interceptor into the Store Controller Class</span></span>

<span data-ttu-id="b6200-190">V této úloze přidáte vlastní filtr tak, že ho vložíte do všech tříd kontroleru a kontrolují akce kontroleru, které budou protokolovány.</span><span class="sxs-lookup"><span data-stu-id="b6200-190">In this task you will add the custom filter by injecting it to all controller classes and controller actions that will be logged.</span></span> <span data-ttu-id="b6200-191">Pro účely tohoto cvičení bude mít třída kontroleru úložiště protokol.</span><span class="sxs-lookup"><span data-stu-id="b6200-191">For the purpose of this exercise, the Store Controller class will have a log.</span></span>

<span data-ttu-id="b6200-192">Metoda **OnActionExecuting** z vlastního filtru **ActionLogFilterAttribute** se spouští při volání vloženého prvku.</span><span class="sxs-lookup"><span data-stu-id="b6200-192">The method **OnActionExecuting** from **ActionLogFilterAttribute** custom filter runs when an injected element is called.</span></span>

<span data-ttu-id="b6200-193">Je také možné zachytit konkrétní metodu kontroleru.</span><span class="sxs-lookup"><span data-stu-id="b6200-193">It is also possible to intercept a specific controller method.</span></span>

1. <span data-ttu-id="b6200-194">Otevřete **StoreController** na **MvcMusicStore\Controllers** a přidejte odkaz na obor názvů **Filters** :</span><span class="sxs-lookup"><span data-stu-id="b6200-194">Open the **StoreController** at **MvcMusicStore\Controllers** and add a reference to the **Filters** namespace:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. <span data-ttu-id="b6200-195">Vložení vlastního filtru **CustomActionFilter** do třídy **StoreController** přidáním atributu **[CustomActionFilter]** před deklarací třídy.</span><span class="sxs-lookup"><span data-stu-id="b6200-195">Inject the custom filter **CustomActionFilter** into **StoreController** class by adding **[CustomActionFilter]** attribute before the class declaration.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > <span data-ttu-id="b6200-196">Pokud je do třídy kontroleru vložen filtr, jsou také vloženy všechny jeho akce.</span><span class="sxs-lookup"><span data-stu-id="b6200-196">When a filter is injected into a controller class, all its actions are also injected.</span></span> <span data-ttu-id="b6200-197">Chcete-li použít filtr pouze pro sadu akcí, budete muset vložit **[CustomActionFilter]** do každého z nich:</span><span class="sxs-lookup"><span data-stu-id="b6200-197">If you would like to apply the filter only for a set of actions, you would have to inject **[CustomActionFilter]** to each one of them:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="b6200-198">Úloha 3 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="b6200-198">Task 3 - Running the Application</span></span>

<span data-ttu-id="b6200-199">V této úloze otestujete, zda filtr protokolování funguje.</span><span class="sxs-lookup"><span data-stu-id="b6200-199">In this task, you will test that the logging filter is working.</span></span> <span data-ttu-id="b6200-200">Spustíte aplikaci a navštívíte úložiště a pak zkontrolujete protokolované aktivity.</span><span class="sxs-lookup"><span data-stu-id="b6200-200">You will start the application and visit the store, and then you will check logged activities.</span></span>

1. <span data-ttu-id="b6200-201">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="b6200-201">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="b6200-202">Přejděte na **/ActionLog** a zobrazte počáteční stav zobrazení protokolu:</span><span class="sxs-lookup"><span data-stu-id="b6200-202">Browse to **/ActionLog** to see log view initial state:</span></span>

    <span data-ttu-id="b6200-203">![Stav sledování protokolu před aktivitou stránky](aspnet-mvc-4-custom-action-filters/_static/image3.png "Stav sledování protokolu před aktivitou stránky")</span><span class="sxs-lookup"><span data-stu-id="b6200-203">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image3.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="b6200-204">*Stav sledování protokolu před aktivitou stránky*</span><span class="sxs-lookup"><span data-stu-id="b6200-204">*Log tracker status before page activity*</span></span>

   > [!NOTE]
   > <span data-ttu-id="b6200-205">Ve výchozím nastavení se vždy zobrazí jedna položka, která je generována při načítání existujících žánrů pro nabídku.</span><span class="sxs-lookup"><span data-stu-id="b6200-205">By default, it will always show one item that is generated when retrieving the existing genres for the menu.</span></span>
   > 
   > <span data-ttu-id="b6200-206">Pro zjednodušení čistíme tabulku **ActionLog** pokaždé, když se aplikace spustí, takže se zobrazí jenom protokoly jednotlivých ověření daného úkolu.</span><span class="sxs-lookup"><span data-stu-id="b6200-206">For simplicity purposes we're cleaning up the **ActionLog** table each time the application runs so it will only show the logs of each particular task's verification.</span></span>
   > 
   > <span data-ttu-id="b6200-207">Aby bylo možné uložit historický protokol pro všechny akce spouštěné v rámci kontroleru úložiště, může být nutné odebrat následující kód z metody **Session\_Start** (ve třídě **Global. asax** ).</span><span class="sxs-lookup"><span data-stu-id="b6200-207">You might need to remove the following code from the **Session\_Start** method (in the **Global.asax** class), in order to save an historical log for all the actions executed within the Store Controller.</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. <span data-ttu-id="b6200-208">V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.</span><span class="sxs-lookup"><span data-stu-id="b6200-208">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
4. <span data-ttu-id="b6200-209">Přejděte na **/ActionLog** a pokud je protokol prázdný, stiskněte klávesu **F5** , aby se stránka aktualizovala.</span><span class="sxs-lookup"><span data-stu-id="b6200-209">Browse to **/ActionLog** and if the log is empty press **F5** to refresh the page.</span></span> <span data-ttu-id="b6200-210">Ověřte, že byly vaše návštěvy sledovány:</span><span class="sxs-lookup"><span data-stu-id="b6200-210">Check that your visits were tracked:</span></span>

    <span data-ttu-id="b6200-211">![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image4.png "Protokol akcí s protokolem aktivit")</span><span class="sxs-lookup"><span data-stu-id="b6200-211">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image4.png "Action log with activity logged")</span></span>

    <span data-ttu-id="b6200-212">*Protokol akcí s protokolem aktivit*</span><span class="sxs-lookup"><span data-stu-id="b6200-212">*Action log with activity logged*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a><span data-ttu-id="b6200-213">Cvičení 2: Správa více filtrů akcí</span><span class="sxs-lookup"><span data-stu-id="b6200-213">Exercise 2: Managing Multiple Action Filters</span></span>

<span data-ttu-id="b6200-214">V tomto cvičení přidáte druhý filtr vlastní akce do třídy StoreController a definujete konkrétní pořadí, ve kterém budou oba filtry provedeny.</span><span class="sxs-lookup"><span data-stu-id="b6200-214">In this exercise you will add a second Custom Action Filter to the StoreController class and define the specific order in which both filters will be executed.</span></span> <span data-ttu-id="b6200-215">Pak aktualizujete kód pro globální registraci filtru.</span><span class="sxs-lookup"><span data-stu-id="b6200-215">Then you will update the code to register the filter Globally.</span></span>

<span data-ttu-id="b6200-216">Při definování pořadí spouštění filtrů existují různé možnosti, které je potřeba vzít v úvahu.</span><span class="sxs-lookup"><span data-stu-id="b6200-216">There are different options to take into account when defining the Filters' execution order.</span></span> <span data-ttu-id="b6200-217">Například vlastnost Order a rozsah filtrů:</span><span class="sxs-lookup"><span data-stu-id="b6200-217">For example, the Order property and the Filters' scope:</span></span>

<span data-ttu-id="b6200-218">Můžete definovat **Rozsah** pro každý z filtrů, například můžete určit rozsah všech filtrů akcí, které mají být spuštěny v rámci **oboru kontroleru**, a všechny autorizační filtry pro spuštění v **globálním oboru**.</span><span class="sxs-lookup"><span data-stu-id="b6200-218">You can define a **Scope** for each of the Filters, for example, you could scope all the Action Filters to run within the **Controller Scope**, and all Authorization Filters to run in **Global scope**.</span></span> <span data-ttu-id="b6200-219">Obory mají definované pořadí provádění.</span><span class="sxs-lookup"><span data-stu-id="b6200-219">The scopes have a defined execution order.</span></span>

<span data-ttu-id="b6200-220">Každý filtr akcí navíc má vlastnost Order, která se používá k určení pořadí spouštění v oboru filtru.</span><span class="sxs-lookup"><span data-stu-id="b6200-220">Additionally, each action filter has an Order property which is used to determine the execution order in the scope of the filter.</span></span>

<span data-ttu-id="b6200-221">Další informace o pořadí spouštění vlastních filtrů akcí najdete v tomto článku na webu MSDN: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span><span class="sxs-lookup"><span data-stu-id="b6200-221">For more information about Custom Action Filters execution order, please visit this MSDN article: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a><span data-ttu-id="b6200-222">Úloha 1: vytvoření nového filtru vlastních akcí</span><span class="sxs-lookup"><span data-stu-id="b6200-222">Task 1: Creating a new Custom Action Filter</span></span>

<span data-ttu-id="b6200-223">V této úloze vytvoříte nový filtr vlastní akce, který bude vložen do třídy StoreController, takže se naučíte spravovat pořadí provádění filtrů.</span><span class="sxs-lookup"><span data-stu-id="b6200-223">In this task, you will create a new Custom Action Filter to inject into the StoreController class, learning how to manage the execution order of the filters.</span></span>

1. <span data-ttu-id="b6200-224">Otevřete řešení **začít** umístěné ve složce **\Source\Ex02-ManagingMultipleActionFilters\Begin** .</span><span class="sxs-lookup"><span data-stu-id="b6200-224">Open the **Begin** solution located at **\Source\Ex02-ManagingMultipleActionFilters\Begin** folder.</span></span> <span data-ttu-id="b6200-225">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="b6200-225">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="b6200-226">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="b6200-226">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="b6200-227">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b6200-227">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="b6200-228">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="b6200-228">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="b6200-229">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="b6200-229">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

        > [!NOTE]
        > <span data-ttu-id="b6200-230">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="b6200-230">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="b6200-231">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="b6200-231">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="b6200-232">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="b6200-232">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
        > 
        > <span data-ttu-id="b6200-233">Další informace najdete v tomto článku: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="b6200-233">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="b6200-234">Přidejte novou C# třídu do složky **Filters** a pojmenujte ji *MyNewCustomActionFilter.cs* .</span><span class="sxs-lookup"><span data-stu-id="b6200-234">Add a new C# class into the **Filters** folder and name it *MyNewCustomActionFilter.cs*</span></span>
3. <span data-ttu-id="b6200-235">Otevřete **MyNewCustomActionFilter.cs** a přidejte odkaz na **System. Web. Mvc** a obor názvů **MvcMusicStore. Models** :</span><span class="sxs-lookup"><span data-stu-id="b6200-235">Open **MyNewCustomActionFilter.cs** and add a reference to **System.Web.Mvc** and the **MvcMusicStore.Models** namespace:</span></span>

    <span data-ttu-id="b6200-236">(Fragment kódu – *ASP.NET MVC 4 – filtry vlastních akcí – EX2-MyNewCustomActionFilterNamespaces*)</span><span class="sxs-lookup"><span data-stu-id="b6200-236">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterNamespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. <span data-ttu-id="b6200-237">Nahraďte výchozí deklaraci třídy následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="b6200-237">Replace the default class declaration with the following code.</span></span>

    <span data-ttu-id="b6200-238">(Fragment kódu – *ASP.NET MVC 4 – filtry vlastních akcí – EX2-MyNewCustomActionFilterClass*)</span><span class="sxs-lookup"><span data-stu-id="b6200-238">(Code Snippet - *ASP.NET MVC 4 Custom Action Filters - Ex2-MyNewCustomActionFilterClass*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="b6200-239">Tento filtr vlastní akce je skoro stejný než ten, který jste vytvořili v předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="b6200-239">This Custom Action Filter is almost the same than the one you created in the previous exercise.</span></span> <span data-ttu-id="b6200-240">Hlavním rozdílem je, že má *&quot;protokolovaná&quot;* atributem s tímto novým názvem Class, který identifikuje, který filtr zaregistroval protokol.</span><span class="sxs-lookup"><span data-stu-id="b6200-240">The main difference is that it has the *&quot;Logged By&quot;* attribute updated with this new class' name to identify which filter registered the log.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a><span data-ttu-id="b6200-241">Úkol 2: vložení nového Zachytávosti kódu do třídy StoreController</span><span class="sxs-lookup"><span data-stu-id="b6200-241">Task 2: Injecting a new Code Interceptor into the StoreController Class</span></span>

<span data-ttu-id="b6200-242">V této úloze přidáte nový vlastní filtr do třídy StoreController a spustíte řešení, abyste ověřili, jak oba filtry vzájemně spolupracují.</span><span class="sxs-lookup"><span data-stu-id="b6200-242">In this task, you will add a new custom filter into the StoreController Class and run the solution to verify how both filters work together.</span></span>

1. <span data-ttu-id="b6200-243">Otevřete třídu **StoreController** umístěnou na adrese **MvcMusicStore\Controllers** a vložením nového vlastního filtru **MyNewCustomActionFilter** do třídy **StoreController** , jako je znázorněno v následujícím kódu.</span><span class="sxs-lookup"><span data-stu-id="b6200-243">Open the **StoreController** class located at **MvcMusicStore\Controllers** and inject the new custom filter **MyNewCustomActionFilter** into **StoreController** class like is shown in the following code.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. <span data-ttu-id="b6200-244">Nyní spusťte aplikaci, abyste viděli, jak tyto dvě filtry vlastní akce fungují.</span><span class="sxs-lookup"><span data-stu-id="b6200-244">Now, run the application in order to see how these two Custom Action Filters work.</span></span> <span data-ttu-id="b6200-245">Pokud to chcete provést, stiskněte klávesu **F5** a počkejte, dokud se aplikace nespustí.</span><span class="sxs-lookup"><span data-stu-id="b6200-245">To do this, press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="b6200-246">Přejděte na **/ActionLog** a zobrazte počáteční stav zobrazení protokolu.</span><span class="sxs-lookup"><span data-stu-id="b6200-246">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="b6200-247">![Stav sledování protokolu před aktivitou stránky](aspnet-mvc-4-custom-action-filters/_static/image5.png "Stav sledování protokolu před aktivitou stránky")</span><span class="sxs-lookup"><span data-stu-id="b6200-247">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image5.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="b6200-248">*Stav sledování protokolu před aktivitou stránky*</span><span class="sxs-lookup"><span data-stu-id="b6200-248">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="b6200-249">V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.</span><span class="sxs-lookup"><span data-stu-id="b6200-249">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="b6200-250">Ověřte, že tento čas; vaše návštěvy byly sledovány dvakrát: jednou pro každý z vlastních filtrů akcí, které jste přidali ve třídě **StorageController** .</span><span class="sxs-lookup"><span data-stu-id="b6200-250">Check that this time; your visits were tracked twice: once for each of the Custom Action Filters you added in the **StorageController** class.</span></span>

    <span data-ttu-id="b6200-251">![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image6.png "Protokol akcí s protokolem aktivit")</span><span class="sxs-lookup"><span data-stu-id="b6200-251">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image6.png "Action log with activity logged")</span></span>

    <span data-ttu-id="b6200-252">*Protokol akcí s protokolem aktivit*</span><span class="sxs-lookup"><span data-stu-id="b6200-252">*Action log with activity logged*</span></span>
6. <span data-ttu-id="b6200-253">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="b6200-253">Close the browser.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a><span data-ttu-id="b6200-254">Úloha 3: Správa řazení filtru</span><span class="sxs-lookup"><span data-stu-id="b6200-254">Task 3: Managing Filter Ordering</span></span>

<span data-ttu-id="b6200-255">V této úloze se dozvíte, jak spravovat pořadí spouštění filtrů pomocí vlastnosti Order.</span><span class="sxs-lookup"><span data-stu-id="b6200-255">In this task, you will learn how to manage the filters' execution order by using the Order property.</span></span>

1. <span data-ttu-id="b6200-256">Otevřete třídu **StoreController** umístěnou na adrese **MvcMusicStore\Controllers** a určete vlastnost **Order** v obou filtrech, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="b6200-256">Open the **StoreController** class located at **MvcMusicStore\Controllers** and specify the **Order** property in both filters like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. <span data-ttu-id="b6200-257">Nyní ověřte, jak jsou filtry spouštěny v závislosti na hodnotě vlastnosti pořadí.</span><span class="sxs-lookup"><span data-stu-id="b6200-257">Now, verify how the filters are executed depending on its Order property's value.</span></span> <span data-ttu-id="b6200-258">Zjistíte, že filtr s nejmenší hodnotou objednávky (**CustomActionFilter**) je první spuštěný.</span><span class="sxs-lookup"><span data-stu-id="b6200-258">You will find that the filter with the smallest Order value (**CustomActionFilter**) is the first one that is executed.</span></span> <span data-ttu-id="b6200-259">Stiskněte klávesu **F5** a počkejte, dokud se aplikace nespustí.</span><span class="sxs-lookup"><span data-stu-id="b6200-259">Press **F5** and wait until the application starts.</span></span>
3. <span data-ttu-id="b6200-260">Přejděte na **/ActionLog** a zobrazte počáteční stav zobrazení protokolu.</span><span class="sxs-lookup"><span data-stu-id="b6200-260">Browse to **/ActionLog** to see log view initial state.</span></span>

    <span data-ttu-id="b6200-261">![Stav sledování protokolu před aktivitou stránky](aspnet-mvc-4-custom-action-filters/_static/image7.png "Stav sledování protokolu před aktivitou stránky")</span><span class="sxs-lookup"><span data-stu-id="b6200-261">![Log tracker status before page activity](aspnet-mvc-4-custom-action-filters/_static/image7.png "Log tracker status before page activity")</span></span>

    <span data-ttu-id="b6200-262">*Stav sledování protokolu před aktivitou stránky*</span><span class="sxs-lookup"><span data-stu-id="b6200-262">*Log tracker status before page activity*</span></span>
4. <span data-ttu-id="b6200-263">V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.</span><span class="sxs-lookup"><span data-stu-id="b6200-263">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
5. <span data-ttu-id="b6200-264">Ověřte, že v tuto chvíli byly vaše návštěvy sledovány seřazené podle hodnoty pořadí filtrů: **CustomActionFilter** Logs.</span><span class="sxs-lookup"><span data-stu-id="b6200-264">Check that this time, your visits were tracked ordered by the filters' Order value: **CustomActionFilter** logs' first.</span></span>

    <span data-ttu-id="b6200-265">![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image8.png "Protokol akcí s protokolem aktivit")</span><span class="sxs-lookup"><span data-stu-id="b6200-265">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image8.png "Action log with activity logged")</span></span>

    <span data-ttu-id="b6200-266">*Protokol akcí s protokolem aktivit*</span><span class="sxs-lookup"><span data-stu-id="b6200-266">*Action log with activity logged*</span></span>
6. <span data-ttu-id="b6200-267">Nyní aktualizujete hodnotu pořadí filtrů a ověříte způsob, jakým se mění pořadí protokolování.</span><span class="sxs-lookup"><span data-stu-id="b6200-267">Now, you will update the Filters' order value and verify how the logging order changes.</span></span> <span data-ttu-id="b6200-268">Ve třídě **StoreController** aktualizujte hodnotu objednávky filters, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="b6200-268">In the **StoreController** class, update the Filters' Order value like shown below.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. <span data-ttu-id="b6200-269">Spusťte aplikaci znovu stisknutím klávesy **F5**.</span><span class="sxs-lookup"><span data-stu-id="b6200-269">Run the application again by pressing **F5**.</span></span>
8. <span data-ttu-id="b6200-270">V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.</span><span class="sxs-lookup"><span data-stu-id="b6200-270">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
9. <span data-ttu-id="b6200-271">Ověřte, že se nejprve zobrazí protokoly vytvořené filtrem **MyNewCustomActionFilter** .</span><span class="sxs-lookup"><span data-stu-id="b6200-271">Check that this time, the logs created by **MyNewCustomActionFilter** filter appears first.</span></span>

    <span data-ttu-id="b6200-272">![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image9.png "Protokol akcí s protokolem aktivit")</span><span class="sxs-lookup"><span data-stu-id="b6200-272">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image9.png "Action log with activity logged")</span></span>

    <span data-ttu-id="b6200-273">*Protokol akcí s protokolem aktivit*</span><span class="sxs-lookup"><span data-stu-id="b6200-273">*Action log with activity logged*</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a><span data-ttu-id="b6200-274">Úloha 4: globální registrace filtrů</span><span class="sxs-lookup"><span data-stu-id="b6200-274">Task 4: Registering Filters Globally</span></span>

<span data-ttu-id="b6200-275">V této úloze aktualizujete řešení a zaregistrujete nový filtr (**MyNewCustomActionFilter**) jako globální filtr.</span><span class="sxs-lookup"><span data-stu-id="b6200-275">In this task, you will update the solution to register the new filter (**MyNewCustomActionFilter**) as a global filter.</span></span> <span data-ttu-id="b6200-276">Tím dojde k aktivaci všemi akcemi provedenými v aplikaci a nikoli pouze v StoreController, jako u předchozí úlohy.</span><span class="sxs-lookup"><span data-stu-id="b6200-276">By doing this, it will be triggered by all the actions performed in the application and not only in the StoreController ones as in the previous task.</span></span>

1. <span data-ttu-id="b6200-277">Ve třídě **StoreController** odeberte atribut **[MyNewCustomActionFilter]** a vlastnost Order z **[CustomActionFilter]** .</span><span class="sxs-lookup"><span data-stu-id="b6200-277">In **StoreController** class, remove **[MyNewCustomActionFilter]** attribute and the order property from **[CustomActionFilter]**.</span></span> <span data-ttu-id="b6200-278">Měl by vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="b6200-278">It should look like the following:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. <span data-ttu-id="b6200-279">Otevřete soubor **Global. asax** a vyhledejte **aplikaci\_spustit** metodu.</span><span class="sxs-lookup"><span data-stu-id="b6200-279">Open **Global.asax** file and locate the **Application\_Start** method.</span></span> <span data-ttu-id="b6200-280">Všimněte si, že při každém spuštění aplikace se registruje globální filtry voláním metody **RegisterGlobalFilters** v rámci třídy **FilterConfig** .</span><span class="sxs-lookup"><span data-stu-id="b6200-280">Notice that each time the application starts it is registering the global filters by calling **RegisterGlobalFilters** method within **FilterConfig** class.</span></span>

    <span data-ttu-id="b6200-281">![Globální filtry se registrují v Global. asax.](aspnet-mvc-4-custom-action-filters/_static/image10.png "Globální filtry se registrují v Global. asax.")</span><span class="sxs-lookup"><span data-stu-id="b6200-281">![Registering Global Filters in Global.asax](aspnet-mvc-4-custom-action-filters/_static/image10.png "Registering Global Filters in Global.asax")</span></span>

    <span data-ttu-id="b6200-282">*Globální filtry se registrují v Global. asax.*</span><span class="sxs-lookup"><span data-stu-id="b6200-282">*Registering Global Filters in Global.asax*</span></span>
3. <span data-ttu-id="b6200-283">Otevřete soubor **FilterConfig.cs** ve složce **App\_Start** .</span><span class="sxs-lookup"><span data-stu-id="b6200-283">Open **FilterConfig.cs** file within **App\_Start** folder.</span></span>
4. <span data-ttu-id="b6200-284">Přidat odkaz na použití System. Web. Mvc; použití MvcMusicStore. filters; hosting.</span><span class="sxs-lookup"><span data-stu-id="b6200-284">Add a reference to using System.Web.Mvc; using MvcMusicStore.Filters; namespace.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. <span data-ttu-id="b6200-285">Aktualizujte metodu **RegisterGlobalFilters** přidáním vlastního filtru.</span><span class="sxs-lookup"><span data-stu-id="b6200-285">Update **RegisterGlobalFilters** method adding your custom filter.</span></span> <span data-ttu-id="b6200-286">Chcete-li to provést, přidejte zvýrazněný kód:</span><span class="sxs-lookup"><span data-stu-id="b6200-286">To do this, add the highlighted code:</span></span>

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. <span data-ttu-id="b6200-287">Spusťte aplikaci stisknutím klávesy **F5**.</span><span class="sxs-lookup"><span data-stu-id="b6200-287">Run the application by pressing **F5**.</span></span>
7. <span data-ttu-id="b6200-288">V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.</span><span class="sxs-lookup"><span data-stu-id="b6200-288">Click one of the **Genres** from the menu and perform some actions there, like browsing an available album.</span></span>
8. <span data-ttu-id="b6200-289">Ověřte, zda je nyní **[MyNewCustomActionFilter]** vloženo v HomeController a ActionLogController.</span><span class="sxs-lookup"><span data-stu-id="b6200-289">Check that now **[MyNewCustomActionFilter]** is being injected in HomeController and ActionLogController too.</span></span>

    <span data-ttu-id="b6200-290">![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image11.png "Protokol akcí s protokolem aktivit")</span><span class="sxs-lookup"><span data-stu-id="b6200-290">![Action log with activity logged](aspnet-mvc-4-custom-action-filters/_static/image11.png "Action log with activity logged")</span></span>

    <span data-ttu-id="b6200-291">*Protokol akcí s protokolem globálních aktivit*</span><span class="sxs-lookup"><span data-stu-id="b6200-291">*Action log with global activity logged*</span></span>

> [!NOTE]
> <span data-ttu-id="b6200-292">Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure podle [dodatku B: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="b6200-292">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="b6200-293">Souhrn</span><span class="sxs-lookup"><span data-stu-id="b6200-293">Summary</span></span>

<span data-ttu-id="b6200-294">Vyplněním tohoto praktického cvičení jste zjistili, jak roztáhnout filtr akcí, aby bylo možné provádět vlastní akce.</span><span class="sxs-lookup"><span data-stu-id="b6200-294">By completing this Hands-On Lab you have learned how to extend an action filter to execute custom actions.</span></span> <span data-ttu-id="b6200-295">Také jste se naučili, jak vložit libovolný filtr na vaše řadiče stránky.</span><span class="sxs-lookup"><span data-stu-id="b6200-295">You have also learned how to inject any filter to your page controllers.</span></span> <span data-ttu-id="b6200-296">Použily se následující koncepty:</span><span class="sxs-lookup"><span data-stu-id="b6200-296">The following concepts were used:</span></span>

- <span data-ttu-id="b6200-297">Jak vytvořit vlastní filtry akcí pomocí třídy ASP.NET MVC ActionFilterAttribute</span><span class="sxs-lookup"><span data-stu-id="b6200-297">How to create Custom Action filters with the ASP.NET MVC ActionFilterAttribute class</span></span>
- <span data-ttu-id="b6200-298">Vložení filtrů do řadičů ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b6200-298">How to inject filters into ASP.NET MVC controllers</span></span>
- <span data-ttu-id="b6200-299">Jak spravovat řazení filtrů pomocí vlastnosti Order</span><span class="sxs-lookup"><span data-stu-id="b6200-299">How to manage filter ordering using the Order property</span></span>
- <span data-ttu-id="b6200-300">Globální registraci filtrů</span><span class="sxs-lookup"><span data-stu-id="b6200-300">How to register filters globally</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="b6200-301">Příloha A: instalace Visual Studio Express 2012 pro web</span><span class="sxs-lookup"><span data-stu-id="b6200-301">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="b6200-302">**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="b6200-302">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="b6200-303">Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="b6200-303">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="b6200-304">Přejděte do [ (Nastavení)https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) (Integrace a služby).</span><span class="sxs-lookup"><span data-stu-id="b6200-304">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="b6200-305">Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="b6200-305">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="b6200-306">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="b6200-306">Click on **Install Now**.</span></span> <span data-ttu-id="b6200-307">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="b6200-307">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="b6200-308">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="b6200-308">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="b6200-309">![Nainstalovat Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="b6200-309">![Install Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="b6200-310">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="b6200-310">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="b6200-311">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="b6200-311">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí licenčních podmínek](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    <span data-ttu-id="b6200-313">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="b6200-313">*Accepting the license terms*</span></span>
5. <span data-ttu-id="b6200-314">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="b6200-314">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    <span data-ttu-id="b6200-316">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="b6200-316">*Installation progress*</span></span>
6. <span data-ttu-id="b6200-317">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="b6200-317">When the installation completes, click **Finish**.</span></span>

    ![Instalace dokončena](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    <span data-ttu-id="b6200-319">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="b6200-319">*Installation completed*</span></span>
7. <span data-ttu-id="b6200-320">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="b6200-320">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="b6200-321">Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .</span><span class="sxs-lookup"><span data-stu-id="b6200-321">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Dlaždice VS Express for Web](aspnet-mvc-4-custom-action-filters/_static/image16.png)

    <span data-ttu-id="b6200-323">*Dlaždice VS Express for Web*</span><span class="sxs-lookup"><span data-stu-id="b6200-323">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="b6200-324">Příloha B: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="b6200-324">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="b6200-325">V tomto dodatku se dozvíte, jak vytvořit nový web z Windows Azure Portál pro správu a jak publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce Nasazení webu pro publikování poskytované službou Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b6200-325">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="b6200-326">Úloha 1 – Vytvoření nového webu z portálu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="b6200-326">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="b6200-327">Přejít na [portál pro správu Windows Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="b6200-327">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6200-328">S Windows Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu.</span><span class="sxs-lookup"><span data-stu-id="b6200-328">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="b6200-329">[Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.</span><span class="sxs-lookup"><span data-stu-id="b6200-329">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="b6200-330">![Přihlaste se k Windows Azure Portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Přihlaste se k Windows Azure Portal")</span><span class="sxs-lookup"><span data-stu-id="b6200-330">![Log on to Windows Azure portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="b6200-331">*Přihlášení k Windows Azure Portál pro správu*</span><span class="sxs-lookup"><span data-stu-id="b6200-331">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="b6200-332">Na panelu příkazů klikněte na **Nový** .</span><span class="sxs-lookup"><span data-stu-id="b6200-332">Click **New** on the command bar.</span></span>

    <span data-ttu-id="b6200-333">![Vytvoření nového webu](aspnet-mvc-4-custom-action-filters/_static/image18.png "Vytvoření nového webu")</span><span class="sxs-lookup"><span data-stu-id="b6200-333">![Creating a new Web Site](aspnet-mvc-4-custom-action-filters/_static/image18.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="b6200-334">*Vytvoření nového webu*</span><span class="sxs-lookup"><span data-stu-id="b6200-334">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="b6200-335">Klikněte na **compute** | **Web**.</span><span class="sxs-lookup"><span data-stu-id="b6200-335">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="b6200-336">Pak vyberte možnost **rychlé vytvoření** .</span><span class="sxs-lookup"><span data-stu-id="b6200-336">Then select **Quick Create** option.</span></span> <span data-ttu-id="b6200-337">Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.</span><span class="sxs-lookup"><span data-stu-id="b6200-337">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6200-338">Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat.</span><span class="sxs-lookup"><span data-stu-id="b6200-338">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="b6200-339">Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál.</span><span class="sxs-lookup"><span data-stu-id="b6200-339">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="b6200-340">Nezahrnuje kroky pro nastavení databáze.</span><span class="sxs-lookup"><span data-stu-id="b6200-340">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="b6200-341">![Vytvoření nového webu pomocí rychlého vytvoření](aspnet-mvc-4-custom-action-filters/_static/image19.png "Vytvoření nového webu pomocí rychlého vytvoření")</span><span class="sxs-lookup"><span data-stu-id="b6200-341">![Creating a new Web Site using Quick Create](aspnet-mvc-4-custom-action-filters/_static/image19.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="b6200-342">*Vytvoření nového webu pomocí rychlého vytvoření*</span><span class="sxs-lookup"><span data-stu-id="b6200-342">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="b6200-343">Počkejte, než se nový **Web** vytvoří.</span><span class="sxs-lookup"><span data-stu-id="b6200-343">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="b6200-344">Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** .</span><span class="sxs-lookup"><span data-stu-id="b6200-344">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="b6200-345">Ověřte, zda nový web funguje.</span><span class="sxs-lookup"><span data-stu-id="b6200-345">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="b6200-346">![Procházení na nový web](aspnet-mvc-4-custom-action-filters/_static/image20.png "Procházení na nový web")</span><span class="sxs-lookup"><span data-stu-id="b6200-346">![Browsing to the new web site](aspnet-mvc-4-custom-action-filters/_static/image20.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="b6200-347">*Procházení na nový web*</span><span class="sxs-lookup"><span data-stu-id="b6200-347">*Browsing to the new web site*</span></span>

    <span data-ttu-id="b6200-348">![Běžící Web](aspnet-mvc-4-custom-action-filters/_static/image21.png "Běžící Web")</span><span class="sxs-lookup"><span data-stu-id="b6200-348">![Web site running](aspnet-mvc-4-custom-action-filters/_static/image21.png "Web site running")</span></span>

    <span data-ttu-id="b6200-349">*Běžící Web*</span><span class="sxs-lookup"><span data-stu-id="b6200-349">*Web site running*</span></span>
6. <span data-ttu-id="b6200-350">Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="b6200-350">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="b6200-351">![Otevření stránek správy webu](aspnet-mvc-4-custom-action-filters/_static/image22.png "Otevření stránek správy webu")</span><span class="sxs-lookup"><span data-stu-id="b6200-351">![Opening the web site management pages](aspnet-mvc-4-custom-action-filters/_static/image22.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="b6200-352">*Otevření stránek správy webu*</span><span class="sxs-lookup"><span data-stu-id="b6200-352">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="b6200-353">Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .</span><span class="sxs-lookup"><span data-stu-id="b6200-353">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6200-354">*Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace.</span><span class="sxs-lookup"><span data-stu-id="b6200-354">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="b6200-355">Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace.</span><span class="sxs-lookup"><span data-stu-id="b6200-355">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="b6200-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b6200-356">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="b6200-357">![Stahuje se publikační profil webu.](aspnet-mvc-4-custom-action-filters/_static/image23.png "Stahuje se publikační profil webu.")</span><span class="sxs-lookup"><span data-stu-id="b6200-357">![Downloading the web site publish profile](aspnet-mvc-4-custom-action-filters/_static/image23.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="b6200-358">*Stahuje se publikační profil webu.*</span><span class="sxs-lookup"><span data-stu-id="b6200-358">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="b6200-359">Stáhněte si soubor profilu publikování do známého umístění.</span><span class="sxs-lookup"><span data-stu-id="b6200-359">Download the publish profile file to a known location.</span></span> <span data-ttu-id="b6200-360">V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6200-360">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="b6200-361">![Ukládání souboru profilu publikování](aspnet-mvc-4-custom-action-filters/_static/image24.png "Ukládá se publikační profil.")</span><span class="sxs-lookup"><span data-stu-id="b6200-361">![Saving the publish profile file](aspnet-mvc-4-custom-action-filters/_static/image24.png "Saving the publish profile")</span></span>

    <span data-ttu-id="b6200-362">*Ukládání souboru profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="b6200-362">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="b6200-363">Úloha 2 – Konfigurace databázového serveru</span><span class="sxs-lookup"><span data-stu-id="b6200-363">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="b6200-364">Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="b6200-364">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="b6200-365">Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.</span><span class="sxs-lookup"><span data-stu-id="b6200-365">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="b6200-366">Pro uložení aplikační databáze budete potřebovat server SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b6200-366">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="b6200-367">SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**.</span><span class="sxs-lookup"><span data-stu-id="b6200-367">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="b6200-368">Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="b6200-368">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="b6200-369">Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách.</span><span class="sxs-lookup"><span data-stu-id="b6200-369">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="b6200-370">Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.</span><span class="sxs-lookup"><span data-stu-id="b6200-370">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="b6200-371">![Řídicí panel serveru SQL Database](aspnet-mvc-4-custom-action-filters/_static/image25.png "Řídicí panel serveru SQL Database")</span><span class="sxs-lookup"><span data-stu-id="b6200-371">![SQL Database Server Dashboard](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="b6200-372">*Řídicí panel serveru SQL Database*</span><span class="sxs-lookup"><span data-stu-id="b6200-372">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="b6200-373">V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru.</span><span class="sxs-lookup"><span data-stu-id="b6200-373">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="b6200-374">Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](aspnet-mvc-4-custom-action-filters/_static/image26.png).</span><span class="sxs-lookup"><span data-stu-id="b6200-374">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-custom-action-filters/_static/image26.png) button.</span></span>

    ![Přidává se IP adresa klienta.](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    <span data-ttu-id="b6200-376">*Přidává se IP adresa klienta.*</span><span class="sxs-lookup"><span data-stu-id="b6200-376">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="b6200-377">Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="b6200-377">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Potvrdit změny](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    <span data-ttu-id="b6200-379">*Potvrdit změny*</span><span class="sxs-lookup"><span data-stu-id="b6200-379">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="b6200-380">Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="b6200-380">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="b6200-381">Vraťte se do řešení ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="b6200-381">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="b6200-382">V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="b6200-382">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="b6200-383">![Publikování aplikace](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publikování aplikace")</span><span class="sxs-lookup"><span data-stu-id="b6200-383">![Publishing the Application](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publishing the Application")</span></span>

    <span data-ttu-id="b6200-384">*Publikování webu*</span><span class="sxs-lookup"><span data-stu-id="b6200-384">*Publishing the web site*</span></span>
2. <span data-ttu-id="b6200-385">Importujte profil publikování, který jste uložili v prvním úkolu.</span><span class="sxs-lookup"><span data-stu-id="b6200-385">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="b6200-386">![Import profilu publikování](aspnet-mvc-4-custom-action-filters/_static/image30.png "Import profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="b6200-386">![Importing the publish profile](aspnet-mvc-4-custom-action-filters/_static/image30.png "Importing the publish profile")</span></span>

    <span data-ttu-id="b6200-387">*Importuje se publikační profil.*</span><span class="sxs-lookup"><span data-stu-id="b6200-387">*Importing publish profile*</span></span>
3. <span data-ttu-id="b6200-388">Klikněte na **ověřit připojení**.</span><span class="sxs-lookup"><span data-stu-id="b6200-388">Click **Validate Connection**.</span></span> <span data-ttu-id="b6200-389">Po dokončení ověřování klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="b6200-389">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6200-390">Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.</span><span class="sxs-lookup"><span data-stu-id="b6200-390">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="b6200-391">![Ověřování připojení](aspnet-mvc-4-custom-action-filters/_static/image31.png "Ověřování připojení")</span><span class="sxs-lookup"><span data-stu-id="b6200-391">![Validating connection](aspnet-mvc-4-custom-action-filters/_static/image31.png "Validating connection")</span></span>

    <span data-ttu-id="b6200-392">*Ověřování připojení*</span><span class="sxs-lookup"><span data-stu-id="b6200-392">*Validating connection*</span></span>
4. <span data-ttu-id="b6200-393">Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="b6200-393">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="b6200-394">![Konfigurace nasazení webu](aspnet-mvc-4-custom-action-filters/_static/image32.png "Konfigurace nasazení webu")</span><span class="sxs-lookup"><span data-stu-id="b6200-394">![Web deploy configuration](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web deploy configuration")</span></span>

    <span data-ttu-id="b6200-395">*Konfigurace nasazení webu*</span><span class="sxs-lookup"><span data-stu-id="b6200-395">*Web deploy configuration*</span></span>
5. <span data-ttu-id="b6200-396">Připojení k databázi nakonfigurujte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="b6200-396">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="b6200-397">Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="b6200-397">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="b6200-398">V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="b6200-398">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="b6200-399">V **heslo** zadejte přihlašovací heslo správce serveru.</span><span class="sxs-lookup"><span data-stu-id="b6200-399">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="b6200-400">Zadejte nový název databáze.</span><span class="sxs-lookup"><span data-stu-id="b6200-400">Type a new database name.</span></span>

     <span data-ttu-id="b6200-401">![Konfigurace cílového připojovacího řetězce](aspnet-mvc-4-custom-action-filters/_static/image33.png "Konfigurace cílového připojovacího řetězce")</span><span class="sxs-lookup"><span data-stu-id="b6200-401">![Configuring destination connection string](aspnet-mvc-4-custom-action-filters/_static/image33.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="b6200-402">*Konfigurace cílového připojovacího řetězce*</span><span class="sxs-lookup"><span data-stu-id="b6200-402">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="b6200-403">Pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6200-403">Then click **OK**.</span></span> <span data-ttu-id="b6200-404">Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="b6200-404">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="b6200-405">![Vytvoření databáze](aspnet-mvc-4-custom-action-filters/_static/image34.png "Vytváří se řetězec databáze.")</span><span class="sxs-lookup"><span data-stu-id="b6200-405">![Creating the database](aspnet-mvc-4-custom-action-filters/_static/image34.png "Creating the database string")</span></span>

    <span data-ttu-id="b6200-406">*Vytvoření databáze*</span><span class="sxs-lookup"><span data-stu-id="b6200-406">*Creating the database*</span></span>
7. <span data-ttu-id="b6200-407">Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení.</span><span class="sxs-lookup"><span data-stu-id="b6200-407">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="b6200-408">Pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="b6200-408">Then click **Next**.</span></span>

    <span data-ttu-id="b6200-409">![Připojovací řetězec ukazující na SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Připojovací řetězec ukazující na SQL Database")</span><span class="sxs-lookup"><span data-stu-id="b6200-409">![Connection string pointing to SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="b6200-410">*Připojovací řetězec ukazující na SQL Database*</span><span class="sxs-lookup"><span data-stu-id="b6200-410">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="b6200-411">Na stránce **Náhled** klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="b6200-411">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="b6200-412">![Publikování webové aplikace](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publikování webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="b6200-412">![Publishing the web application](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publishing the web application")</span></span>

    <span data-ttu-id="b6200-413">*Publikování webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="b6200-413">*Publishing the web application*</span></span>
9. <span data-ttu-id="b6200-414">Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.</span><span class="sxs-lookup"><span data-stu-id="b6200-414">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="b6200-415">Příloha C: používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="b6200-415">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="b6200-416">S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="b6200-416">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="b6200-417">Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="b6200-417">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="b6200-418">![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-custom-action-filters/_static/image37.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="b6200-418">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-custom-action-filters/_static/image37.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="b6200-419">*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="b6200-419">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="b6200-420">***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***</span><span class="sxs-lookup"><span data-stu-id="b6200-420">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="b6200-421">Umístěte kurzor na místo, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="b6200-421">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="b6200-422">Začněte psát název fragmentu (bez mezer a spojovníků).</span><span class="sxs-lookup"><span data-stu-id="b6200-422">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="b6200-423">Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="b6200-423">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="b6200-424">Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).</span><span class="sxs-lookup"><span data-stu-id="b6200-424">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="b6200-425">Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="b6200-425">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="b6200-426">![Začněte psát název fragmentu.](aspnet-mvc-4-custom-action-filters/_static/image38.png "Začněte psát název fragmentu.")</span><span class="sxs-lookup"><span data-stu-id="b6200-426">![Start typing the snippet name](aspnet-mvc-4-custom-action-filters/_static/image38.png "Start typing the snippet name")</span></span>

<span data-ttu-id="b6200-427">*Začněte psát název fragmentu.*</span><span class="sxs-lookup"><span data-stu-id="b6200-427">*Start typing the snippet name*</span></span>

<span data-ttu-id="b6200-428">![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-custom-action-filters/_static/image39.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")</span><span class="sxs-lookup"><span data-stu-id="b6200-428">![Press Tab to select the highlighted snippet](aspnet-mvc-4-custom-action-filters/_static/image39.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="b6200-429">*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*</span><span class="sxs-lookup"><span data-stu-id="b6200-429">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="b6200-430">![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-custom-action-filters/_static/image40.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")</span><span class="sxs-lookup"><span data-stu-id="b6200-430">![Press Tab again and the snippet will expand](aspnet-mvc-4-custom-action-filters/_static/image40.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="b6200-431">*Stiskněte znovu TAB a fragment kódu se rozšíří.*</span><span class="sxs-lookup"><span data-stu-id="b6200-431">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="b6200-432">***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první.</span><span class="sxs-lookup"><span data-stu-id="b6200-432">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="b6200-433">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="b6200-433">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="b6200-434">Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="b6200-434">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="b6200-435">Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="b6200-435">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="b6200-436">![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-custom-action-filters/_static/image41.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")</span><span class="sxs-lookup"><span data-stu-id="b6200-436">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-custom-action-filters/_static/image41.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="b6200-437">*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*</span><span class="sxs-lookup"><span data-stu-id="b6200-437">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="b6200-438">![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-custom-action-filters/_static/image42.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")</span><span class="sxs-lookup"><span data-stu-id="b6200-438">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-custom-action-filters/_static/image42.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="b6200-439">*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*</span><span class="sxs-lookup"><span data-stu-id="b6200-439">*Pick the relevant snippet from the list, by clicking on it*</span></span>
