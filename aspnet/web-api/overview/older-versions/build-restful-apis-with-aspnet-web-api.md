---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: Sestavení rozhraní API RESTful s webovým rozhraním API ASP.NET – ASP.NET 4. x
author: rick-anderson
description: 'Praktická cvičení: k vytvoření jednoduchého REST API pro aplikaci Správce kontaktů použijte webové rozhraní API v ASP.NET 4. x.'
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621812"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a><span data-ttu-id="a8345-103">Sestavení rozhraní API RESTful s webovým rozhraním API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a8345-103">Build RESTful APIs with ASP.NET Web API</span></span>

<span data-ttu-id="a8345-104">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="a8345-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="a8345-105">Praktická cvičení: k vytvoření jednoduchého REST API pro aplikaci Správce kontaktů použijte webové rozhraní API v ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="a8345-105">Hands on lab: Use Web API in ASP.NET 4.x to build a simple REST API for a contact manager application.</span></span> <span data-ttu-id="a8345-106">Také vytvoříte klienta pro využívání rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-106">You will also build a client to consume the API.</span></span>

<span data-ttu-id="a8345-107">V posledních letech se stala jasné, že HTTP není jenom pro obsluhu stránek HTML.</span><span class="sxs-lookup"><span data-stu-id="a8345-107">In recent years, it has become clear that HTTP is not just for serving up HTML pages.</span></span> <span data-ttu-id="a8345-108">Je to také výkonná platforma pro vytváření webových rozhraní API pomocí několik příkazů (GET, POST a tak dále) a několika jednoduchých konceptů, jako jsou *identifikátory URI* a *hlavičky*.</span><span class="sxs-lookup"><span data-stu-id="a8345-108">It is also a powerful platform for building Web APIs, using a handful of verbs (GET, POST, and so forth) plus a few simple concepts such as *URIs* and *headers*.</span></span> <span data-ttu-id="a8345-109">Webové rozhraní API ASP.NET je sada komponent, které zjednodušují programování HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8345-109">ASP.NET Web API is a set of components that simplify HTTP programming.</span></span> <span data-ttu-id="a8345-110">Vzhledem k tomu, že je postaven na ASP.NET MVC runtime, webové rozhraní API automaticky zpracovává podrobnosti o přenosech nízké úrovně HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8345-110">Because it is built on top of the ASP.NET MVC runtime, Web API automatically handles the low-level transport details of HTTP.</span></span> <span data-ttu-id="a8345-111">Zároveň webové rozhraní API přirozeně zpřístupňuje model programování HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8345-111">At the same time, Web API naturally exposes the HTTP programming model.</span></span> <span data-ttu-id="a8345-112">Jedním z cílů webového rozhraní API je fakt, že se *nejedná o* realitu protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8345-112">In fact, one goal of Web API is to *not* abstract away the reality of HTTP.</span></span> <span data-ttu-id="a8345-113">V důsledku toho je webové rozhraní API flexibilní a snadno širší.</span><span class="sxs-lookup"><span data-stu-id="a8345-113">As a result, Web API is both flexible and easy to extend.</span></span>  <span data-ttu-id="a8345-114">Styl architektury REST byl ověřen jako efektivní způsob, jak využít protokol HTTP, přestože není určitě jediným platným přístupem k HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8345-114">The REST architectural style has proven to be an effective way to leverage HTTP - although it is certainly not the only valid approach to HTTP.</span></span> <span data-ttu-id="a8345-115">Správce kontaktů zveřejní RESTful pro výpis, přidávání a odebírání kontaktů, a to i mimo jiné.</span><span class="sxs-lookup"><span data-stu-id="a8345-115">The contact manager will expose the RESTful for listing, adding and removing contacts, among others.</span></span> 

<span data-ttu-id="a8345-116">Toto testovací prostředí vyžaduje základní znalost protokolu HTTP, REST a předpokládá, že máte základní znalosti o jazycích HTML, JavaScript a jQuery.</span><span class="sxs-lookup"><span data-stu-id="a8345-116">This lab requires a basic understanding of HTTP, REST, and assumes you have a basic working knowledge of HTML, JavaScript, and jQuery.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="a8345-117">Web ASP.NET má v [https://asp.net/web-api](https://asp.net/web-api)oblast vyhrazenou pro rozhraní Web API pro ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a8345-117">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [https://asp.net/web-api](https://asp.net/web-api).</span></span> <span data-ttu-id="a8345-118">Tato lokalita bude dál poskytovat nejnovější informace, ukázky a novinky související s webovým rozhraním API, proto je pravidelně kontrolovat, pokud byste chtěli vytvořit vlastní webová rozhraní API, která jsou dostupná prakticky pro zařízení nebo vývojové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a8345-118">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>
> > 
> > <span data-ttu-id="a8345-119">Webové rozhraní API ASP.NET, podobně jako ASP.NET MVC 4, má skvělou flexibilitu v podobě oddělení vrstvy služeb od řadičů, což vám umožní využít několik dostupných rozhraní pro vkládání závislostí poměrně snadno.</span><span class="sxs-lookup"><span data-stu-id="a8345-119">ASP.NET Web API, similar to ASP.NET MVC 4, has great flexibility in terms of separating the service layer from the controllers allowing you to use several of the available Dependency Injection frameworks fairly easy.</span></span> <span data-ttu-id="a8345-120">Na webu MSDN je dobrá ukázka, která ukazuje, jak používat Ninject pro vkládání závislostí v projektu webového rozhraní API ASP.NET, který si můžete stáhnout [tady](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span><span class="sxs-lookup"><span data-stu-id="a8345-120">There is a good sample in MSDN that shows how to use Ninject for dependency injection in an ASP.NET Web API project that you can download it from [here](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7).</span></span>
> 
> 
> <span data-ttu-id="a8345-121">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="a8345-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="a8345-122">Cíle</span><span class="sxs-lookup"><span data-stu-id="a8345-122">Objectives</span></span>

<span data-ttu-id="a8345-123">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="a8345-123">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="a8345-124">Implementace webového rozhraní API RESTful</span><span class="sxs-lookup"><span data-stu-id="a8345-124">Implement a RESTful Web API</span></span>
- <span data-ttu-id="a8345-125">Volání rozhraní API z klienta HTML</span><span class="sxs-lookup"><span data-stu-id="a8345-125">Call the API from an HTML client</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="a8345-126">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="a8345-126">Prerequisites</span></span>

<span data-ttu-id="a8345-127">Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:</span><span class="sxs-lookup"><span data-stu-id="a8345-127">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="a8345-128">[Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nejvyšší (pokyny k instalaci najdete v [příloze B](#AppendixB) ).</span><span class="sxs-lookup"><span data-stu-id="a8345-128">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="a8345-129">Nastavení</span><span class="sxs-lookup"><span data-stu-id="a8345-129">Setup</span></span>

<span data-ttu-id="a8345-130">**Instalace fragmentů kódu**</span><span class="sxs-lookup"><span data-stu-id="a8345-130">**Installing Code Snippets**</span></span>

<span data-ttu-id="a8345-131">Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8345-131">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="a8345-132">Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .</span><span class="sxs-lookup"><span data-stu-id="a8345-132">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="a8345-133">Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze A: používání fragmentů kódu](#AppendixA)&quot;.</span><span class="sxs-lookup"><span data-stu-id="a8345-133">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="a8345-134">Cvičení</span><span class="sxs-lookup"><span data-stu-id="a8345-134">Exercises</span></span>

<span data-ttu-id="a8345-135">Tato praktická cvičení zahrnuje následující cvičení:</span><span class="sxs-lookup"><span data-stu-id="a8345-135">This hands-on lab includes the following exercise:</span></span>

1. [<span data-ttu-id="a8345-136">Cvičení 1: Vytvoření webového rozhraní API jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="a8345-136">Exercise 1: Create a Read-Only Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="a8345-137">Cvičení 2: Vytvoření webového rozhraní API pro čtení i zápis</span><span class="sxs-lookup"><span data-stu-id="a8345-137">Exercise 2: Create a Read/Write Web API</span></span>](#Exercise2)
3. [<span data-ttu-id="a8345-138">Cvičení 3: využívání webového rozhraní API z klienta HTML</span><span class="sxs-lookup"><span data-stu-id="a8345-138">Exercise 3: Consume the Web API from an HTML Client</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="a8345-139">Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení.</span><span class="sxs-lookup"><span data-stu-id="a8345-139">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="a8345-140">Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.</span><span class="sxs-lookup"><span data-stu-id="a8345-140">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="a8345-141">Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.</span><span class="sxs-lookup"><span data-stu-id="a8345-141">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a><span data-ttu-id="a8345-142">Cvičení 1: Vytvoření webového rozhraní API jen pro čtení</span><span class="sxs-lookup"><span data-stu-id="a8345-142">Exercise 1: Create a Read-Only Web API</span></span>

<span data-ttu-id="a8345-143">V tomto cvičení budete implementovat metody GET jen pro čtení pro správce kontaktů.</span><span class="sxs-lookup"><span data-stu-id="a8345-143">In this exercise, you will implement the read-only GET methods for the contact manager.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a><span data-ttu-id="a8345-144">Úloha 1 – Vytvoření projektu rozhraní API</span><span class="sxs-lookup"><span data-stu-id="a8345-144">Task 1 - Creating the API Project</span></span>

<span data-ttu-id="a8345-145">V této úloze použijete nové šablony webového projektu ASP.NET k vytvoření webové aplikace webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-145">In this task, you will use the new ASP.NET web project templates to create a Web API web application.</span></span>

1. <span data-ttu-id="a8345-146">Spusťte **Visual Studio 2012 Express for Web**. to uděláte tak, že přejdete na **Start** a zadáte **vs Express for Web** a pak stisknete **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a8345-146">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="a8345-147">V nabídce **soubor** vyberte možnost **Nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="a8345-147">From the **File** menu, select **New Project**.</span></span> <span data-ttu-id="a8345-148">Vyberte **vizuál C# | Typ webového** projektu ze stromového zobrazení typu projektu a pak vyberte typ projektu **webové aplikace ASP.NET MVC 4** .</span><span class="sxs-lookup"><span data-stu-id="a8345-148">Select the **Visual C# | Web** project type from the project type tree view, then select the **ASP.NET MVC 4 Web Application** project type.</span></span> <span data-ttu-id="a8345-149">Nastavte **název** projektu na *ContactManager* a *začněte* **název řešení** a potom klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8345-149">Set the project's **Name** to *ContactManager* and the **Solution name** to *Begin*, then click **OK**.</span></span>

    <span data-ttu-id="a8345-150">![Vytvoření nového projektu webové aplikace ASP.NET MVC 4,0](build-restful-apis-with-aspnet-web-api/_static/image1.png "Vytvoření nového projektu webové aplikace ASP.NET MVC 4,0")</span><span class="sxs-lookup"><span data-stu-id="a8345-150">![Creating a new ASP.NET MVC 4.0 Web Application Project](build-restful-apis-with-aspnet-web-api/_static/image1.png "Creating a new ASP.NET MVC 4.0 Web Application Project")</span></span>

    <span data-ttu-id="a8345-151">*Vytvoření nového projektu webové aplikace ASP.NET MVC 4,0*</span><span class="sxs-lookup"><span data-stu-id="a8345-151">*Creating a new ASP.NET MVC 4.0 Web Application Project*</span></span>
3. <span data-ttu-id="a8345-152">V dialogovém okně ASP.NET MVC 4 – typ projektu vyberte typ projektu **webové rozhraní API** .</span><span class="sxs-lookup"><span data-stu-id="a8345-152">In the ASP.NET MVC 4 project type dialog, select the **Web API** project type.</span></span> <span data-ttu-id="a8345-153">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8345-153">Click **OK**.</span></span>

    <span data-ttu-id="a8345-154">![Určení typu projektu webového rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image2.png "Určení typu projektu webového rozhraní API")</span><span class="sxs-lookup"><span data-stu-id="a8345-154">![Specifying the Web API project type](build-restful-apis-with-aspnet-web-api/_static/image2.png "Specifying the Web API project type")</span></span>

    <span data-ttu-id="a8345-155">*Určení typu projektu webového rozhraní API*</span><span class="sxs-lookup"><span data-stu-id="a8345-155">*Specifying the Web API project type*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a><span data-ttu-id="a8345-156">Úloha 2 – vytvoření řadičů rozhraní API pro správce kontaktů</span><span class="sxs-lookup"><span data-stu-id="a8345-156">Task 2 - Creating the Contact Manager API Controllers</span></span>

<span data-ttu-id="a8345-157">V této úloze vytvoříte třídy kontroleru, ve kterých se budou nacházet metody rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-157">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="a8345-158">Odstraňte soubor s názvem **ValuesController.cs** v rámci složky **Controllers** z projektu.</span><span class="sxs-lookup"><span data-stu-id="a8345-158">Delete the file named **ValuesController.cs** within **Controllers** folder from the project.</span></span>
2. <span data-ttu-id="a8345-159">Klikněte pravým tlačítkem na složku **řadiče** v projektu a vyberte **Přidat | Kontroler** z kontextové nabídky</span><span class="sxs-lookup"><span data-stu-id="a8345-159">Right-click the **Controllers** folder in the project and select **Add | Controller** from the context menu.</span></span>

    <span data-ttu-id="a8345-160">![Přidání nového kontroleru do projektu](build-restful-apis-with-aspnet-web-api/_static/image3.png "Přidání nového kontroleru do projektu")</span><span class="sxs-lookup"><span data-stu-id="a8345-160">![Adding a new controller to the project](build-restful-apis-with-aspnet-web-api/_static/image3.png "Adding a new controller to the project")</span></span>

    <span data-ttu-id="a8345-161">*Přidání nového kontroleru do projektu*</span><span class="sxs-lookup"><span data-stu-id="a8345-161">*Adding a new controller to the project*</span></span>
3. <span data-ttu-id="a8345-162">V dialogovém okně **Přidat řadič** , které se zobrazí, v nabídce šablona vyberte **prázdný kontroler rozhraní API** .</span><span class="sxs-lookup"><span data-stu-id="a8345-162">In the **Add Controller** dialog that appears, select **Empty API Controller** from the Template menu.</span></span> <span data-ttu-id="a8345-163">Pojmenujte třídu Controller **ContactController**.</span><span class="sxs-lookup"><span data-stu-id="a8345-163">Name the controller class **ContactController**.</span></span> <span data-ttu-id="a8345-164">Pak klikněte na tlačítko **Přidat.**</span><span class="sxs-lookup"><span data-stu-id="a8345-164">Then, click **Add.**</span></span>

    <span data-ttu-id="a8345-165">![Použití dialogového okna přidat řadič k vytvoření nového kontroleru webového rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image4.png "Použití dialogového okna přidat řadič k vytvoření nového kontroleru webového rozhraní API")</span><span class="sxs-lookup"><span data-stu-id="a8345-165">![Using the Add Controller dialog to create a new Web API controller](build-restful-apis-with-aspnet-web-api/_static/image4.png "Using the Add Controller dialog to create a new Web API controller")</span></span>

    <span data-ttu-id="a8345-166">*Použití dialogového okna přidat řadič k vytvoření nového kontroleru webového rozhraní API*</span><span class="sxs-lookup"><span data-stu-id="a8345-166">*Using the Add Controller dialog to create a new Web API controller*</span></span>
4. <span data-ttu-id="a8345-167">Do **ContactController**přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="a8345-167">Add the following code to the **ContactController**.</span></span>

    <span data-ttu-id="a8345-168">(Fragment kódu – *Web API Lab – Ex01-get – metoda rozhraní API*)</span><span class="sxs-lookup"><span data-stu-id="a8345-168">(Code Snippet - *Web API Lab - Ex01 - Get API Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. <span data-ttu-id="a8345-169">Stisknutím klávesy **F5** spusťte ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="a8345-169">Press **F5** to debug the application.</span></span> <span data-ttu-id="a8345-170">Měla by se zobrazit výchozí domovská stránka projektu webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-170">The default home page for a Web API project should appear.</span></span>

    <span data-ttu-id="a8345-171">![Výchozí domovská stránka aplikace webového rozhraní API ASP.NET](build-restful-apis-with-aspnet-web-api/_static/image5.png "Výchozí domovská stránka aplikace webového rozhraní API ASP.NET")</span><span class="sxs-lookup"><span data-stu-id="a8345-171">![The default home page of an ASP.NET Web API application](build-restful-apis-with-aspnet-web-api/_static/image5.png "The default home page of an ASP.NET Web API application")</span></span>

    <span data-ttu-id="a8345-172">*Výchozí domovská stránka aplikace webového rozhraní API ASP.NET*</span><span class="sxs-lookup"><span data-stu-id="a8345-172">*The default home page of an ASP.NET Web API application*</span></span>
6. <span data-ttu-id="a8345-173">V okně Internet Exploreru stisknutím klávesy **F12** otevřete okno **vývojářské nástroje** .</span><span class="sxs-lookup"><span data-stu-id="a8345-173">In the Internet Explorer window, press the **F12** key to open the **Developer Tools** window.</span></span> <span data-ttu-id="a8345-174">Klikněte na kartu **síť** a potom kliknutím na tlačítko **Spustit digitalizaci** zahajte zachytávání síťového provozu do okna.</span><span class="sxs-lookup"><span data-stu-id="a8345-174">Click the **Network** tab, and then click the **Start Capturing** button to begin capturing network traffic into the window.</span></span>

    <span data-ttu-id="a8345-175">![Otevření karty síť a inicializace síťového zachytávání](build-restful-apis-with-aspnet-web-api/_static/image6.png "Otevření karty síť a inicializace síťového zachytávání")</span><span class="sxs-lookup"><span data-stu-id="a8345-175">![Opening the network tab and initiating network capture](build-restful-apis-with-aspnet-web-api/_static/image6.png "Opening the network tab and initiating network capture")</span></span>

    <span data-ttu-id="a8345-176">*Otevření karty síť a inicializace síťového zachytávání*</span><span class="sxs-lookup"><span data-stu-id="a8345-176">*Opening the network tab and initiating network capture*</span></span>
7. <span data-ttu-id="a8345-177">Přidejte adresu URL do panelu Adresa v prohlížeči pomocí **/API/Contact** a stiskněte klávesu ENTER.</span><span class="sxs-lookup"><span data-stu-id="a8345-177">Append the URL in the browser's address bar with **/api/contact** and press enter.</span></span> <span data-ttu-id="a8345-178">Podrobnosti o přenosu se zobrazí v okně zachytávání sítě.</span><span class="sxs-lookup"><span data-stu-id="a8345-178">The transmission details will appear in the network capture window.</span></span> <span data-ttu-id="a8345-179">Všimněte si, že typ MIME odpovědi je **Application/JSON**.</span><span class="sxs-lookup"><span data-stu-id="a8345-179">Note that the response's MIME type is **application/json**.</span></span> <span data-ttu-id="a8345-180">Ukazuje, jak výchozí výstupní formát je JSON.</span><span class="sxs-lookup"><span data-stu-id="a8345-180">This demonstrates how the default output format is JSON.</span></span>

    <span data-ttu-id="a8345-181">![Zobrazení výstupu požadavku webového rozhraní API v zobrazení sítě](build-restful-apis-with-aspnet-web-api/_static/image7.png "Zobrazení výstupu požadavku webového rozhraní API v zobrazení sítě")</span><span class="sxs-lookup"><span data-stu-id="a8345-181">![Viewing the output of the Web API request in the Network view](build-restful-apis-with-aspnet-web-api/_static/image7.png "Viewing the output of the Web API request in the Network view")</span></span>

    <span data-ttu-id="a8345-182">*Zobrazení výstupu požadavku webového rozhraní API v zobrazení sítě*</span><span class="sxs-lookup"><span data-stu-id="a8345-182">*Viewing the output of the Web API request in the Network view*</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8345-183">Výchozí chování aplikace Internet Explorer 10 v tomto okamžiku bude dotázáno, zda by uživatel chtěl uložit nebo otevřít datový proud, který je výsledkem volání webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-183">Internet Explorer 10's default behavior at this point will be to ask if the user would like to save or open the stream resulting from the Web API call.</span></span> <span data-ttu-id="a8345-184">Výstupem bude textový soubor, který obsahuje výsledek JSON volání adresy URL webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-184">The output will be a text file containing the JSON result of the Web API URL call.</span></span> <span data-ttu-id="a8345-185">Nezavírejte dialog, aby bylo možné sledovat obsah odpovědi prostřednictvím okna nástrojů pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="a8345-185">Do not cancel the dialog in order to be able to watch the response's content through Developers Tool window.</span></span>
8. <span data-ttu-id="a8345-186">Kliknutím na tlačítko **Přejít k podrobnému zobrazení** zobrazíte další podrobnosti o odezvě tohoto volání rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-186">Click the **Go to detailed view** button to see more details about the response of this API call.</span></span>

    <span data-ttu-id="a8345-187">![Přepnout do podrobného zobrazení](build-restful-apis-with-aspnet-web-api/_static/image8.png "Přepnout na zobrazení podrobností")</span><span class="sxs-lookup"><span data-stu-id="a8345-187">![Switch to Detailed View](build-restful-apis-with-aspnet-web-api/_static/image8.png "Switch to Details View")</span></span>

    <span data-ttu-id="a8345-188">*Přepnout do podrobného zobrazení*</span><span class="sxs-lookup"><span data-stu-id="a8345-188">*Switch to Detailed View*</span></span>
9. <span data-ttu-id="a8345-189">Chcete-li zobrazit skutečný text odpovědi JSON, klikněte na kartu **tělo odpovědi** .</span><span class="sxs-lookup"><span data-stu-id="a8345-189">Click the **Response body** tab to view the actual JSON response text.</span></span>

    <span data-ttu-id="a8345-190">![Zobrazení výstupního textu JSON v monitorování sítě](build-restful-apis-with-aspnet-web-api/_static/image9.png "Zobrazení výstupního textu JSON v monitorování sítě")</span><span class="sxs-lookup"><span data-stu-id="a8345-190">![Viewing the JSON output text in the network monitor](build-restful-apis-with-aspnet-web-api/_static/image9.png "Viewing the JSON output text in the network monitor")</span></span>

    <span data-ttu-id="a8345-191">*Zobrazení výstupního textu JSON v monitorování sítě*</span><span class="sxs-lookup"><span data-stu-id="a8345-191">*Viewing the JSON output text in the network monitor*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a><span data-ttu-id="a8345-192">Úloha 3 – vytvoření modelů kontaktů a rozšíření Správce kontaktů</span><span class="sxs-lookup"><span data-stu-id="a8345-192">Task 3 - Creating the Contact Models and Augment the Contact Controller</span></span>

<span data-ttu-id="a8345-193">V této úloze vytvoříte třídy kontroleru, ve kterých se budou nacházet metody rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-193">In this task, you will create the controller classes in which API methods will reside.</span></span>

1. <span data-ttu-id="a8345-194">Klikněte pravým tlačítkem na složku **modely** a vyberte **Přidat | Třída...** z místní nabídky.</span><span class="sxs-lookup"><span data-stu-id="a8345-194">Right-click the **Models** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="a8345-195">![Přidání nového modelu do webové aplikace](build-restful-apis-with-aspnet-web-api/_static/image10.png "Přidání nového modelu do webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="a8345-195">![Adding a new model to the web application](build-restful-apis-with-aspnet-web-api/_static/image10.png "Adding a new model to the web application")</span></span>

    <span data-ttu-id="a8345-196">*Přidání nového modelu do webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="a8345-196">*Adding a new model to the web application*</span></span>
2. <span data-ttu-id="a8345-197">V dialogovém okně **Přidat novou položku** pojmenujte nový soubor **Contact.cs** a klikněte na **Přidat.**</span><span class="sxs-lookup"><span data-stu-id="a8345-197">In the **Add New Item** dialog, name the new file **Contact.cs** and click **Add.**</span></span>

    <span data-ttu-id="a8345-198">![Vytváření nového souboru třídy kontaktů](build-restful-apis-with-aspnet-web-api/_static/image11.png "Vytváření nového souboru třídy kontaktů")</span><span class="sxs-lookup"><span data-stu-id="a8345-198">![Creating the new Contact class file](build-restful-apis-with-aspnet-web-api/_static/image11.png "Creating the new Contact class file")</span></span>

    <span data-ttu-id="a8345-199">*Vytváření nového souboru třídy kontaktů*</span><span class="sxs-lookup"><span data-stu-id="a8345-199">*Creating the new Contact class file*</span></span>
3. <span data-ttu-id="a8345-200">Do třídy **Contact** přidejte následující zvýrazněný kód.</span><span class="sxs-lookup"><span data-stu-id="a8345-200">Add the following highlighted code to the **Contact** class.</span></span>

    <span data-ttu-id="a8345-201">(Fragment kódu – *Web API Lab-Ex01-Contact Class*)</span><span class="sxs-lookup"><span data-stu-id="a8345-201">(Code Snippet - *Web API Lab - Ex01 - Contact Class*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. <span data-ttu-id="a8345-202">Ve třídě **ContactController** vyberte textový **řetězec** v definici metody metody **Get** a zadejte *kontaktní*text.</span><span class="sxs-lookup"><span data-stu-id="a8345-202">In the **ContactController** class, select the word **string** in method definition of the **Get** method, and type the word *Contact*.</span></span> <span data-ttu-id="a8345-203">Po zadání slova se na začátku **kontaktu**slov zobrazí indikátor.</span><span class="sxs-lookup"><span data-stu-id="a8345-203">Once the word is typed in, an indicator will appear at the beginning of the word **Contact**.</span></span> <span data-ttu-id="a8345-204">Buď podržte stisknutou klávesu **CTRL** , stiskněte klávesu tečka (.), nebo klikněte na ikonu pomocí myši. otevře se dialogové okno pomoc v editoru kódu pro automatické vyplňování direktivy **using** pro obor názvů modelů.</span><span class="sxs-lookup"><span data-stu-id="a8345-204">Either hold down the **Ctrl** key and press the period (.) key or click the icon using your mouse to open up the assistance dialog in the code editor, to automatically fill in the **using** directive for the Models namespace.</span></span>

    ![Použití pomoci IntelliSense pro deklarace oboru názvů](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    <span data-ttu-id="a8345-206">*Použití pomoci IntelliSense pro deklarace oboru názvů*</span><span class="sxs-lookup"><span data-stu-id="a8345-206">*Using Intellisense assistance for namespace declarations*</span></span>
5. <span data-ttu-id="a8345-207">Upravte kód metody **Get** tak, aby vracel pole instancí modelu kontaktu.</span><span class="sxs-lookup"><span data-stu-id="a8345-207">Modify the code for the **Get** method so that it returns an array of Contact model instances.</span></span>

    <span data-ttu-id="a8345-208">(Fragment kódu – *Web API Lab – Ex01 – vrácení seznamu kontaktů*)</span><span class="sxs-lookup"><span data-stu-id="a8345-208">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. <span data-ttu-id="a8345-209">Stiskněte klávesu **F5** pro ladění webové aplikace v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a8345-209">Press **F5** to debug the web application in the browser.</span></span> <span data-ttu-id="a8345-210">Chcete-li zobrazit změny provedené ve výstupu rozhraní API, proveďte následující kroky.</span><span class="sxs-lookup"><span data-stu-id="a8345-210">To view the changes made to the response output of the API, perform the following steps.</span></span>

   1. <span data-ttu-id="a8345-211">Po otevření prohlížeče stiskněte klávesu **F12** , pokud vývojářské nástroje ještě nejsou otevřené.</span><span class="sxs-lookup"><span data-stu-id="a8345-211">Once the browser opens, press **F12** if the developer tools are not open yet.</span></span>
   2. <span data-ttu-id="a8345-212">Klikněte na kartu **síť** .</span><span class="sxs-lookup"><span data-stu-id="a8345-212">Click the **Network** tab.</span></span>
   3. <span data-ttu-id="a8345-213">Stiskněte tlačítko **Spustit záznam** .</span><span class="sxs-lookup"><span data-stu-id="a8345-213">Press the **Start Capturing** button.</span></span>
   4. <span data-ttu-id="a8345-214">Přidejte příponu URL **/API/Contact** k adrese URL v adresním řádku a stiskněte klávesu **ENTER** .</span><span class="sxs-lookup"><span data-stu-id="a8345-214">Add the URL suffix **/api/contact** to the URL in the address bar and press the **Enter** key.</span></span>
   5. <span data-ttu-id="a8345-215">Stiskněte tlačítko **Přejít na podrobné zobrazení** .</span><span class="sxs-lookup"><span data-stu-id="a8345-215">Press the **Go to detailed view** button.</span></span>
   6. <span data-ttu-id="a8345-216">Vyberte kartu **text odpovědi** . Měl by se zobrazit řetězec JSON představující serializovanou formu pole instancí kontaktů.</span><span class="sxs-lookup"><span data-stu-id="a8345-216">Select the **Response body** tab. You should see a JSON string representing the serialized form of an array of Contact instances.</span></span>

      <span data-ttu-id="a8345-217">![Serializovaný výstup pro komplexní volání metody webového rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image13.png "Serializovaný výstup pro komplexní volání metody webového rozhraní API")</span><span class="sxs-lookup"><span data-stu-id="a8345-217">![JSON serialized output of a complex Web API method call](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON serialized output of a complex Web API method call")</span></span>

      <span data-ttu-id="a8345-218">*Serializovaný výstup pro komplexní volání metody webového rozhraní API*</span><span class="sxs-lookup"><span data-stu-id="a8345-218">*JSON serialized output of a complex Web API method call*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a><span data-ttu-id="a8345-219">Úloha 4 – extrakce funkcí do vrstvy služeb</span><span class="sxs-lookup"><span data-stu-id="a8345-219">Task 4 - Extracting Functionality into a Service Layer</span></span>

<span data-ttu-id="a8345-220">Tato úloha demonstruje, jak extrahovat funkce do vrstvy služeb, aby vývojáři mohli snadno oddělit své funkce služby od vrstvy kontroleru, a tím umožnit opětovné použití služeb, které skutečně dělají.</span><span class="sxs-lookup"><span data-stu-id="a8345-220">This task will demonstrate how to extract functionality into a Service layer to make it easy for developers to separate their service functionality from the controller layer, thereby allowing reusability of the services that actually do the work.</span></span>

1. <span data-ttu-id="a8345-221">Vytvořte novou složku v kořenovém adresáři řešení a pojmenujte ji IT **služby**.</span><span class="sxs-lookup"><span data-stu-id="a8345-221">Create a new folder in the solution root and name it **Services**.</span></span> <span data-ttu-id="a8345-222">Provedete to tak, že kliknete pravým tlačítkem na projekt **ContactManager** , vyberete **Přidat** | **novou složku**a pojmenujte IT *služby*.</span><span class="sxs-lookup"><span data-stu-id="a8345-222">To do this, right-click **ContactManager** project, select **Add** | **New Folder**, name it *Services*.</span></span>

    <span data-ttu-id="a8345-223">![Vytváření složky služeb](build-restful-apis-with-aspnet-web-api/_static/image14.png "Vytváření složky služeb")</span><span class="sxs-lookup"><span data-stu-id="a8345-223">![Creating Services folder](build-restful-apis-with-aspnet-web-api/_static/image14.png "Creating Services folder")</span></span>

    <span data-ttu-id="a8345-224">*Vytváření složky služeb*</span><span class="sxs-lookup"><span data-stu-id="a8345-224">*Creating Services folder*</span></span>
2. <span data-ttu-id="a8345-225">Klikněte pravým tlačítkem na složku **služby** a vyberte **Přidat | Třída...** z místní nabídky.</span><span class="sxs-lookup"><span data-stu-id="a8345-225">Right-click the **Services** folder and select **Add | Class...** from the context menu.</span></span>

    <span data-ttu-id="a8345-226">![Přidání nové třídy do složky služby](build-restful-apis-with-aspnet-web-api/_static/image15.png "Přidání nové třídy do složky služby")</span><span class="sxs-lookup"><span data-stu-id="a8345-226">![Adding a new class to the Services folder](build-restful-apis-with-aspnet-web-api/_static/image15.png "Adding a new class to the Services folder")</span></span>

    <span data-ttu-id="a8345-227">*Přidání nové třídy do složky služby*</span><span class="sxs-lookup"><span data-stu-id="a8345-227">*Adding a new class to the Services folder*</span></span>
3. <span data-ttu-id="a8345-228">Jakmile se zobrazí dialogové okno **Přidat novou položku** , pojmenujte novou třídu **ContactRepository** a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="a8345-228">When the **Add New Item** dialog appears, name the new class **ContactRepository** and click **Add**.</span></span>

    <span data-ttu-id="a8345-229">![Vytvoření souboru třídy, který bude obsahovat kód pro vrstvu služby úložiště kontaktů](build-restful-apis-with-aspnet-web-api/_static/image16.png "Vytvoření souboru třídy, který bude obsahovat kód pro vrstvu služby úložiště kontaktů")</span><span class="sxs-lookup"><span data-stu-id="a8345-229">![Creating a class file to contain the code for the Contact Repository service layer](build-restful-apis-with-aspnet-web-api/_static/image16.png "Creating a class file to contain the code for the Contact Repository service layer")</span></span>

    <span data-ttu-id="a8345-230">*Vytvoření souboru třídy, který bude obsahovat kód pro vrstvu služby úložiště kontaktů*</span><span class="sxs-lookup"><span data-stu-id="a8345-230">*Creating a class file to contain the code for the Contact Repository service layer*</span></span>
4. <span data-ttu-id="a8345-231">Přidejte do souboru **ContactRepository.cs** direktivu using, aby zahrnovala obor názvů Models.</span><span class="sxs-lookup"><span data-stu-id="a8345-231">Add a using directive to the **ContactRepository.cs** file to include the models namespace.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. <span data-ttu-id="a8345-232">Do souboru **ContactRepository.cs** přidejte následující zvýrazněný kód, který implementuje metodu GetAllContacts.</span><span class="sxs-lookup"><span data-stu-id="a8345-232">Add the following highlighted code to the **ContactRepository.cs** file to implement GetAllContacts method.</span></span>

    <span data-ttu-id="a8345-233">(Fragment kódu – *Web API Lab – Ex01 – úložiště kontaktů*)</span><span class="sxs-lookup"><span data-stu-id="a8345-233">(Code Snippet - *Web API Lab - Ex01 - Contact Repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. <span data-ttu-id="a8345-234">Otevřete soubor **ContactController.cs** , pokud ještě není otevřený.</span><span class="sxs-lookup"><span data-stu-id="a8345-234">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="a8345-235">Do oddílu deklarace oboru názvů souboru přidejte následující příkaz using.</span><span class="sxs-lookup"><span data-stu-id="a8345-235">Add the following using statement to the namespace declaration section of the file.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. <span data-ttu-id="a8345-236">Přidejte do třídy **ContactController.cs** následující zvýrazněný kód pro přidání soukromého pole reprezentujícího instanci úložiště, aby zbytek členů třídy mohl využít implementaci služby.</span><span class="sxs-lookup"><span data-stu-id="a8345-236">Add the following highlighted code to the **ContactController.cs** class to add a private field to represent the instance of the repository, so that the rest of the class members can make use of the service implementation.</span></span>

    <span data-ttu-id="a8345-237">(Fragment kódu – *Web API Lab-Ex01-Controller kontaktů*)</span><span class="sxs-lookup"><span data-stu-id="a8345-237">(Code Snippet - *Web API Lab - Ex01 - Contact Controller*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. <span data-ttu-id="a8345-238">Změňte metodu **Get** tak, aby používala službu úložiště kontaktů.</span><span class="sxs-lookup"><span data-stu-id="a8345-238">Change the **Get** method so that it makes use of the contact repository service.</span></span>

    <span data-ttu-id="a8345-239">(Fragment kódu – *Web API Lab – Ex01 – vrácení seznamu kontaktů přes úložiště*)</span><span class="sxs-lookup"><span data-stu-id="a8345-239">(Code Snippet - *Web API Lab - Ex01 - Returning a list of contacts via the repository*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. <span data-ttu-id="a8345-240">Vložte zarážku do definice metody **Get** **ContactController**.</span><span class="sxs-lookup"><span data-stu-id="a8345-240">Put a breakpoint on the **ContactController**'s **Get** method definition.</span></span>

   <span data-ttu-id="a8345-241">![Přidání zarážek do kontroleru kontaktů](build-restful-apis-with-aspnet-web-api/_static/image17.png "Přidání zarážek do kontroleru kontaktů")</span><span class="sxs-lookup"><span data-stu-id="a8345-241">![Adding breakpoints to the contact controller](build-restful-apis-with-aspnet-web-api/_static/image17.png "Adding breakpoints to the contact controller")</span></span>

   <span data-ttu-id="a8345-242">*Přidání zarážek do kontroleru kontaktů*</span><span class="sxs-lookup"><span data-stu-id="a8345-242">*Adding breakpoints to the contact controller*</span></span>
11. <span data-ttu-id="a8345-243">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="a8345-243">Press **F5** to run the application.</span></span>
12. <span data-ttu-id="a8345-244">Po otevření prohlížeče stiskněte klávesu **F12** a otevřete nástroje pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="a8345-244">When the browser opens, press **F12** to open the developer tools.</span></span>
13. <span data-ttu-id="a8345-245">Klikněte na kartu **síť** .</span><span class="sxs-lookup"><span data-stu-id="a8345-245">Click the **Network** tab.</span></span>
14. <span data-ttu-id="a8345-246">Klikněte na tlačítko **Spustit zachycení** .</span><span class="sxs-lookup"><span data-stu-id="a8345-246">Click the **Start Capturing** button.</span></span>
15. <span data-ttu-id="a8345-247">Připojením adresy URL v adresním řádku s příponou **/API/Contact** a stisknutím klávesy **ENTER** NAČTĚTE kontroler rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-247">Append the URL in the address bar with the suffix **/api/contact** and press **Enter** to load the API controller.</span></span>
16. <span data-ttu-id="a8345-248">Po zahájení provádění metody **Get** by aplikace Visual Studio 2012 měla provést přerušení.</span><span class="sxs-lookup"><span data-stu-id="a8345-248">Visual Studio 2012 should break once **Get** method begins execution.</span></span>

   <span data-ttu-id="a8345-249">![Přerušení v rámci metody Get](build-restful-apis-with-aspnet-web-api/_static/image18.png "Přerušení v rámci metody Get")</span><span class="sxs-lookup"><span data-stu-id="a8345-249">![Breaking within the Get method](build-restful-apis-with-aspnet-web-api/_static/image18.png "Breaking within the Get method")</span></span>

   <span data-ttu-id="a8345-250">*Přerušení v rámci metody Get*</span><span class="sxs-lookup"><span data-stu-id="a8345-250">*Breaking within the Get method*</span></span>
17. <span data-ttu-id="a8345-251">Pokračujte stisknutím **F5**.</span><span class="sxs-lookup"><span data-stu-id="a8345-251">Press **F5** to continue.</span></span>
18. <span data-ttu-id="a8345-252">Vraťte se do aplikace Internet Explorer, pokud ještě není aktivní.</span><span class="sxs-lookup"><span data-stu-id="a8345-252">Go back to Internet Explorer if it is not already in focus.</span></span> <span data-ttu-id="a8345-253">Poznamenejte si okno zachycení sítě.</span><span class="sxs-lookup"><span data-stu-id="a8345-253">Note the network capture window.</span></span>

    <span data-ttu-id="a8345-254">![Zobrazení sítě v aplikaci Internet Explorer zobrazující výsledky volání webového rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image19.png "Zobrazení sítě v aplikaci Internet Explorer zobrazující výsledky volání webového rozhraní API")</span><span class="sxs-lookup"><span data-stu-id="a8345-254">![Network view in Internet Explorer showing results of the Web API call](build-restful-apis-with-aspnet-web-api/_static/image19.png "Network view in Internet Explorer showing results of the Web API call")</span></span>

    <span data-ttu-id="a8345-255">*Zobrazení sítě v aplikaci Internet Explorer zobrazující výsledky volání webového rozhraní API*</span><span class="sxs-lookup"><span data-stu-id="a8345-255">*Network view in Internet Explorer showing results of the Web API call*</span></span>
19. <span data-ttu-id="a8345-256">Klikněte na tlačítko **Přejít k podrobnému zobrazení** .</span><span class="sxs-lookup"><span data-stu-id="a8345-256">Click the **Go to detailed view** button.</span></span>
20. <span data-ttu-id="a8345-257">Klikněte na kartu **tělo odpovědi** . Všimněte si výstupu JSON volání rozhraní API a způsobu, jakým představuje dva kontakty načtené vrstvou služby.</span><span class="sxs-lookup"><span data-stu-id="a8345-257">Click the **Response body** tab. Note the JSON output of the API call, and how it represents the two contacts retrieved by the service layer.</span></span>

    <span data-ttu-id="a8345-258">![Zobrazení výstupu JSON z webového rozhraní API v okně vývojářské nástroje](build-restful-apis-with-aspnet-web-api/_static/image20.png "Zobrazení výstupu JSON z webového rozhraní API v okně vývojářské nástroje")</span><span class="sxs-lookup"><span data-stu-id="a8345-258">![Viewing the JSON output from the Web API in the developer tools window](build-restful-apis-with-aspnet-web-api/_static/image20.png "Viewing the JSON output from the Web API in the developer tools window")</span></span>

    <span data-ttu-id="a8345-259">*Zobrazení výstupu JSON z webového rozhraní API v okně vývojářské nástroje*</span><span class="sxs-lookup"><span data-stu-id="a8345-259">*Viewing the JSON output from the Web API in the developer tools window*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a><span data-ttu-id="a8345-260">Cvičení 2: Vytvoření webového rozhraní API pro čtení i zápis</span><span class="sxs-lookup"><span data-stu-id="a8345-260">Exercise 2: Create a Read/Write Web API</span></span>

<span data-ttu-id="a8345-261">V tomto cvičení budete implementovat metody POST a PUT pro správce kontaktů a povolit tak funkce pro úpravy dat.</span><span class="sxs-lookup"><span data-stu-id="a8345-261">In this exercise, you will implement POST and PUT methods for the contact manager to enable it with data-editing features.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a><span data-ttu-id="a8345-262">Úloha 1 – otevření projektu webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="a8345-262">Task 1 - Opening the Web API Project</span></span>

<span data-ttu-id="a8345-263">V této úloze se připravíte na vylepšení projektu webového rozhraní API vytvořeného v cvičení 1 tak, aby mohl přijímat vstupy uživatele.</span><span class="sxs-lookup"><span data-stu-id="a8345-263">In this task, you will prepare to enhance the Web API project created in Exercise 1 so that it can accept user input.</span></span>

1. <span data-ttu-id="a8345-264">Spusťte **Visual Studio 2012 Express for Web**. to uděláte tak, že přejdete na **Start** a zadáte **vs Express for Web** a pak stisknete **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a8345-264">Run **Visual Studio 2012 Express for Web**, to do this go to **Start** and type **VS Express for Web** then press **Enter**.</span></span>
2. <span data-ttu-id="a8345-265">Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex02-ReadWriteWebAPI/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="a8345-265">Open the **Begin** solution located at **Source/Ex02-ReadWriteWebAPI/Begin/** folder.</span></span> <span data-ttu-id="a8345-266">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="a8345-266">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="a8345-267">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="a8345-267">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="a8345-268">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a8345-268">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="a8345-269">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="a8345-269">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="a8345-270">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="a8345-270">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="a8345-271">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="a8345-271">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="a8345-272">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="a8345-272">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="a8345-273">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="a8345-273">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="a8345-274">Otevřete soubor **Services/ContactRepository. cs** .</span><span class="sxs-lookup"><span data-stu-id="a8345-274">Open the **Services/ContactRepository.cs** file.</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a><span data-ttu-id="a8345-275">Úloha 2 – Přidání funkcí pro trvalost dat do implementace úložiště kontaktů</span><span class="sxs-lookup"><span data-stu-id="a8345-275">Task 2 - Adding Data-Persistence Features to the Contact Repository Implementation</span></span>

<span data-ttu-id="a8345-276">V této úloze budete rozšiřovat třídu ContactRepository projektu webového rozhraní API vytvořeného v cvičení 1 tak, aby mohl zachovávat a přijímat uživatelské vstupy a nové instance kontaktů.</span><span class="sxs-lookup"><span data-stu-id="a8345-276">In this task, you will augment the ContactRepository class of the Web API project created in Exercise 1 so that it can persist and accept user input and new Contact instances.</span></span>

1. <span data-ttu-id="a8345-277">Přidejte následující konstantu do třídy **ContactRepository** , která bude reprezentovat název klíče položky mezipaměti webového serveru později v tomto cvičení.</span><span class="sxs-lookup"><span data-stu-id="a8345-277">Add the following constant to the **ContactRepository** class to represent the name of the web server cache item key name later in this exercise.</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. <span data-ttu-id="a8345-278">Přidejte do **ContactRepository** konstruktor obsahující následující kód.</span><span class="sxs-lookup"><span data-stu-id="a8345-278">Add a constructor to the **ContactRepository** containing the following code.</span></span>

    <span data-ttu-id="a8345-279">(Fragment kódu – *Web API Lab – Ex02 – konstruktor úložiště kontaktů*)</span><span class="sxs-lookup"><span data-stu-id="a8345-279">(Code Snippet - *Web API Lab - Ex02 - Contact Repository Constructor*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. <span data-ttu-id="a8345-280">Upravte kód metody **GetAllContacts** , jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="a8345-280">Modify the code for the **GetAllContacts** method as demonstrated below.</span></span>

    <span data-ttu-id="a8345-281">(Fragment kódu – *Web API Lab-Ex02-get all Contacts*)</span><span class="sxs-lookup"><span data-stu-id="a8345-281">(Code Snippet - *Web API Lab - Ex02 - Get All Contacts*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="a8345-282">Tento příklad je určen pro demonstrační účely a použije mezipaměť webového serveru jako paměťové médium, aby byly hodnoty k dispozici pro více klientů současně, nikoli pro použití mechanismu úložiště relace nebo životnosti úložiště požadavků.</span><span class="sxs-lookup"><span data-stu-id="a8345-282">This example is for demonstration purposes and will use the web server's cache as a storage medium, so that the values will be available to multiple clients simultaneously, rather than use a Session storage mechanism or a Request storage lifetime.</span></span> <span data-ttu-id="a8345-283">Jedním z nich může být místo mezipaměti webového serveru použití Entity Framework, úložiště XML nebo jakékoli jiné odrůdy.</span><span class="sxs-lookup"><span data-stu-id="a8345-283">One could use Entity Framework, XML storage, or any other variety in place of the web server cache.</span></span>
4. <span data-ttu-id="a8345-284">Implementací nové metody s názvem **SaveContact** do třídy **ContactRepository** provedete práci s uložením kontaktu.</span><span class="sxs-lookup"><span data-stu-id="a8345-284">Implement a new method named **SaveContact** to the **ContactRepository** class to do the work of saving a contact.</span></span> <span data-ttu-id="a8345-285">Metoda **SaveContact** by měla mít jeden parametr **kontaktu** a vracet logickou hodnotu, která označuje úspěch nebo neúspěch.</span><span class="sxs-lookup"><span data-stu-id="a8345-285">The **SaveContact** method should take a single **Contact** parameter and return a Boolean value indicating success or failure.</span></span>

    <span data-ttu-id="a8345-286">(Fragment kódu – *Web API Lab-Ex02-implementace metody SaveContact*)</span><span class="sxs-lookup"><span data-stu-id="a8345-286">(Code Snippet - *Web API Lab - Ex02 - Implementing the SaveContact Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a><span data-ttu-id="a8345-287">Cvičení 3: využívání webového rozhraní API z klienta HTML</span><span class="sxs-lookup"><span data-stu-id="a8345-287">Exercise 3: Consume the Web API from an HTML Client</span></span>

<span data-ttu-id="a8345-288">V tomto cvičení vytvoříte klienta HTML, který bude volat webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-288">In this exercise, you will create an HTML client to call the Web API.</span></span> <span data-ttu-id="a8345-289">Tento klient usnadňuje výměnu dat pomocí webového rozhraní API pomocí JavaScriptu a zobrazí výsledky ve webovém prohlížeči pomocí značek HTML.</span><span class="sxs-lookup"><span data-stu-id="a8345-289">This client will facilitate data exchange with the Web API using JavaScript and will display the results in a web browser using HTML markup.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a><span data-ttu-id="a8345-290">Úloha 1 – Změna zobrazení indexu, která poskytuje grafické uživatelské rozhraní pro zobrazování kontaktů</span><span class="sxs-lookup"><span data-stu-id="a8345-290">Task 1 - Modifying the Index View to Provide a GUI for Displaying Contacts</span></span>

<span data-ttu-id="a8345-291">V této úloze upravíte výchozí zobrazení indexu webové aplikace tak, aby podporovalo požadavek zobrazení seznamu existujících kontaktů v prohlížeči HTML.</span><span class="sxs-lookup"><span data-stu-id="a8345-291">In this task, you will modify the default Index view of the web application to support the requirement of displaying the list of existing contacts in an HTML browser.</span></span>

1. <span data-ttu-id="a8345-292">Otevřete **Visual Studio 2012 Express for Web** , pokud ještě není otevřený.</span><span class="sxs-lookup"><span data-stu-id="a8345-292">Open **Visual Studio 2012 Express for Web** if it is not already open.</span></span>
2. <span data-ttu-id="a8345-293">Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex03-ConsumingWebAPI/Begin/** Folder.</span><span class="sxs-lookup"><span data-stu-id="a8345-293">Open the **Begin** solution located at **Source/Ex03-ConsumingWebAPI/Begin/** folder.</span></span> <span data-ttu-id="a8345-294">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="a8345-294">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="a8345-295">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="a8345-295">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="a8345-296">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a8345-296">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="a8345-297">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="a8345-297">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="a8345-298">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="a8345-298">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="a8345-299">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="a8345-299">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="a8345-300">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="a8345-300">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="a8345-301">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="a8345-301">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="a8345-302">Otevřete soubor **index. cshtml** umístěný v **zobrazeních nebo v domovské** složce.</span><span class="sxs-lookup"><span data-stu-id="a8345-302">Open the **Index.cshtml** file located at **Views/Home** folder.</span></span>
4. <span data-ttu-id="a8345-303">Nahraďte kód HTML v prvku div **textem** ID, aby vypadal jako následující kód.</span><span class="sxs-lookup"><span data-stu-id="a8345-303">Replace the HTML code within the div element with id **body** so that it looks like the following code.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. <span data-ttu-id="a8345-304">Přidáním následujícího kódu jazyka JavaScript do dolní části souboru proveďte požadavek HTTP na webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="a8345-304">Add the following Javascript code at the bottom of the file to perform the HTTP request to the Web API.</span></span>

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. <span data-ttu-id="a8345-305">Otevřete soubor **ContactController.cs** , pokud ještě není otevřený.</span><span class="sxs-lookup"><span data-stu-id="a8345-305">Open the **ContactController.cs** file if it is not already open.</span></span>
7. <span data-ttu-id="a8345-306">Umístěte zarážku na metodu **Get** třídy **ContactController** .</span><span class="sxs-lookup"><span data-stu-id="a8345-306">Place a breakpoint on the **Get** method of the **ContactController** class.</span></span>

    <span data-ttu-id="a8345-307">![Umístění zarážky na metodu Get kontroleru rozhraní API](build-restful-apis-with-aspnet-web-api/_static/image21.png "Umístění zarážky na metodu Get kontroleru rozhraní API")</span><span class="sxs-lookup"><span data-stu-id="a8345-307">![Placing a breakpoint on the Get method of the API controller](build-restful-apis-with-aspnet-web-api/_static/image21.png "Placing a breakpoint on the Get method of the API controller")</span></span>

    <span data-ttu-id="a8345-308">*Umístění zarážky na metodu Get kontroleru rozhraní API*</span><span class="sxs-lookup"><span data-stu-id="a8345-308">*Placing a breakpoint on the Get method of the API controller*</span></span>
8. <span data-ttu-id="a8345-309">Stisknutím klávesy **F5** spusťte projekt.</span><span class="sxs-lookup"><span data-stu-id="a8345-309">Press **F5** to run the project.</span></span> <span data-ttu-id="a8345-310">Prohlížeč načte dokument HTML.</span><span class="sxs-lookup"><span data-stu-id="a8345-310">The browser will load the HTML document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8345-311">Ujistěte se, že procházíte na kořenovou adresu URL vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="a8345-311">Ensure that you are browsing to the root URL of your application.</span></span>
9. <span data-ttu-id="a8345-312">Jakmile se stránka načte a spustí se JavaScript, zarážka se vykoná a spuštění kódu se v kontroleru zastaví.</span><span class="sxs-lookup"><span data-stu-id="a8345-312">Once the page loads and the JavaScript executes, the breakpoint will be hit and the code execution will pause in the controller.</span></span>

    <span data-ttu-id="a8345-313">![Ladění volání webového rozhraní API pomocí VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Ladění volání webového rozhraní API pomocí VS Express for Web")</span><span class="sxs-lookup"><span data-stu-id="a8345-313">![Debugging into the Web API calls using VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image22.png "Debugging into the Web API calls using VS Express for Web")</span></span>

    <span data-ttu-id="a8345-314">*Ladění do volání webového rozhraní API pomocí sady Visual Studio 2012 Express for Web*</span><span class="sxs-lookup"><span data-stu-id="a8345-314">*Debugging into the Web API call using Visual Studio 2012 Express for Web*</span></span>
10. <span data-ttu-id="a8345-315">Chcete-li pokračovat v načítání zobrazení v prohlížeči, odeberte zarážku a stiskněte klávesu **F5** nebo tlačítko **Přejít** na panel nástrojů ladění.</span><span class="sxs-lookup"><span data-stu-id="a8345-315">Remove the breakpoint and press **F5** or the debugging toolbar's **Continue** button to continue loading the view in the browser.</span></span> <span data-ttu-id="a8345-316">Po dokončení volání webového rozhraní API byste měli vidět kontakty vrácené z volání webového rozhraní API zobrazené jako položky seznamu v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a8345-316">Once the Web API call completes you should see the contacts returned from the Web API call displayed as list items in the browser.</span></span>

    <span data-ttu-id="a8345-317">![Výsledky volání rozhraní API zobrazeného v prohlížeči jako položky seznamu](build-restful-apis-with-aspnet-web-api/_static/image23.png "Výsledky volání rozhraní API zobrazeného v prohlížeči jako položky seznamu")</span><span class="sxs-lookup"><span data-stu-id="a8345-317">![Results of the API call displayed in the browser as list items](build-restful-apis-with-aspnet-web-api/_static/image23.png "Results of the API call displayed in the browser as list items")</span></span>

    <span data-ttu-id="a8345-318">*Výsledky volání rozhraní API zobrazeného v prohlížeči jako položky seznamu*</span><span class="sxs-lookup"><span data-stu-id="a8345-318">*Results of the API call displayed in the browser as list items*</span></span>
11. <span data-ttu-id="a8345-319">Zastavit ladění.</span><span class="sxs-lookup"><span data-stu-id="a8345-319">Stop debugging.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a><span data-ttu-id="a8345-320">Úloha 2 – Změna zobrazení indexu pro poskytování uživatelského rozhraní pro vytváření kontaktů</span><span class="sxs-lookup"><span data-stu-id="a8345-320">Task 2 - Modifying the Index View to Provide a GUI for Creating Contacts</span></span>

<span data-ttu-id="a8345-321">V této úloze budete pokračovat v úpravách zobrazení indexu aplikace MVC.</span><span class="sxs-lookup"><span data-stu-id="a8345-321">In this task, you will continue to modify the Index view of the MVC application.</span></span> <span data-ttu-id="a8345-322">Formulář se přidá do stránky HTML, která zachytí uživatelský vstup a pošle ho do webového rozhraní API a vytvoří nový kontakt. Nová metoda webového rozhraní API se pak vytvoří ke shromáždění data z grafického uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a8345-322">A form will be added to the HTML page that will capture user input and send it to the Web API to create a new Contact, and a new Web API controller method will be created to collect date from the GUI.</span></span>

1. <span data-ttu-id="a8345-323">Otevřete soubor **ContactController.cs** .</span><span class="sxs-lookup"><span data-stu-id="a8345-323">Open the **ContactController.cs** file.</span></span>
2. <span data-ttu-id="a8345-324">Přidejte novou metodu do třídy Controller s názvem **post** , jak je znázorněno v následujícím kódu.</span><span class="sxs-lookup"><span data-stu-id="a8345-324">Add a new method to the controller class named **Post** as shown in the following code.</span></span>

    <span data-ttu-id="a8345-325">(Fragment kódu – *Web API Lab-Ex03-post*)</span><span class="sxs-lookup"><span data-stu-id="a8345-325">(Code Snippet - *Web API Lab - Ex03 - Post Method*)</span></span>

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. <span data-ttu-id="a8345-326">Otevřete soubor **index. cshtml** v aplikaci Visual Studio, pokud ještě není otevřený.</span><span class="sxs-lookup"><span data-stu-id="a8345-326">Open the **Index.cshtml** file in Visual Studio if it is not already open.</span></span>
4. <span data-ttu-id="a8345-327">Přidejte kód HTML níže do souboru hned po neuspořádaném seznamu, který jste přidali v předchozím úkolu.</span><span class="sxs-lookup"><span data-stu-id="a8345-327">Add the HTML code below to the file just after the unordered list you added in the previous task.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. <span data-ttu-id="a8345-328">Do elementu script v dolní části dokumentu přidejte následující zvýrazněný kód, který bude zpracovávat události kliknutí tlačítkem, které budou odesílat data do webového rozhraní API pomocí volání HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a8345-328">Within the script element at the bottom of the document, add the following highlighted code to handle button-click events, which will post the data to the Web API using an HTTP POST call.</span></span>

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. <span data-ttu-id="a8345-329">V **ContactController.cs**umístěte zarážku na metodu **post** .</span><span class="sxs-lookup"><span data-stu-id="a8345-329">In **ContactController.cs**, place a breakpoint on the **Post** method.</span></span>
7. <span data-ttu-id="a8345-330">Stisknutím klávesy **F5** spusťte aplikaci v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a8345-330">Press **F5** to run the application in the browser.</span></span>
8. <span data-ttu-id="a8345-331">Jakmile se stránka načte do prohlížeče, zadejte nové jméno a ID kontaktu a klikněte na tlačítko **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="a8345-331">Once the page is loaded in the browser, type in a new contact name and Id and click the **Save** button.</span></span>

    <span data-ttu-id="a8345-332">![Dokument HTML klienta načtený v prohlížeči](build-restful-apis-with-aspnet-web-api/_static/image24.png "Dokument HTML klienta načtený v prohlížeči")</span><span class="sxs-lookup"><span data-stu-id="a8345-332">![The client HTML document loaded in the browser](build-restful-apis-with-aspnet-web-api/_static/image24.png "The client HTML document loaded in the browser")</span></span>

    <span data-ttu-id="a8345-333">*Dokument HTML klienta načtený v prohlížeči*</span><span class="sxs-lookup"><span data-stu-id="a8345-333">*The client HTML document loaded in the browser*</span></span>
9. <span data-ttu-id="a8345-334">Po přerušení okna ladicího programu v metodě **post** se podíváme na vlastnosti parametru **kontakt** .</span><span class="sxs-lookup"><span data-stu-id="a8345-334">When the debugger window breaks in the **Post** method, take a look at the properties of the **contact** parameter.</span></span> <span data-ttu-id="a8345-335">Hodnoty by se měly shodovat s daty, která jste zadali ve formuláři.</span><span class="sxs-lookup"><span data-stu-id="a8345-335">The values should match the data you entered in the form.</span></span>

    <span data-ttu-id="a8345-336">![Objekt kontaktu, který se odesílá do webového rozhraní API z klienta](build-restful-apis-with-aspnet-web-api/_static/image25.png "Objekt kontaktu, který se odesílá do webového rozhraní API z klienta")</span><span class="sxs-lookup"><span data-stu-id="a8345-336">![The Contact object being sent to the Web API from the client](build-restful-apis-with-aspnet-web-api/_static/image25.png "The Contact object being sent to the Web API from the client")</span></span>

    <span data-ttu-id="a8345-337">*Objekt kontaktu, který se odesílá do webového rozhraní API z klienta*</span><span class="sxs-lookup"><span data-stu-id="a8345-337">*The Contact object being sent to the Web API from the client*</span></span>
10. <span data-ttu-id="a8345-338">Projděte metodu v ladicím programu, dokud není vytvořena proměnná **odpovědi** .</span><span class="sxs-lookup"><span data-stu-id="a8345-338">Step through the method in the debugger until the **response** variable has been created.</span></span> <span data-ttu-id="a8345-339">Po kontrole v okně **místní** hodnoty v ladicím programu uvidíte, že byly nastaveny všechny vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="a8345-339">Upon inspection in the **Locals** window in the debugger, you'll see that all the properties have been set.</span></span>

   <span data-ttu-id="a8345-340">![Odpověď po vytvoření v ladicím programu](build-restful-apis-with-aspnet-web-api/_static/image26.png "Odpověď po vytvoření v ladicím programu")</span><span class="sxs-lookup"><span data-stu-id="a8345-340">![The response following creation in the debugger](build-restful-apis-with-aspnet-web-api/_static/image26.png "The response following creation in the debugger")</span></span>

   <span data-ttu-id="a8345-341">*Odpověď po vytvoření v ladicím programu*</span><span class="sxs-lookup"><span data-stu-id="a8345-341">*The response following creation in the debugger*</span></span>
11. <span data-ttu-id="a8345-342">Pokud stisknete klávesu **F5** nebo kliknete na **pokračovat** v ladicím programu, požadavek se dokončí.</span><span class="sxs-lookup"><span data-stu-id="a8345-342">If you press **F5** or click **Continue** in the debugger the request will complete.</span></span> <span data-ttu-id="a8345-343">Po přepnutí zpátky do prohlížeče se nový kontakt přidal do seznamu kontaktů uložených implementací **ContactRepository** .</span><span class="sxs-lookup"><span data-stu-id="a8345-343">Once you switch back to the browser, the new contact has been added to the list of contacts stored by the **ContactRepository** implementation.</span></span>

   <span data-ttu-id="a8345-344">![Prohlížeč odráží úspěšné vytvoření nové instance kontaktu.](build-restful-apis-with-aspnet-web-api/_static/image27.png "Prohlížeč odráží úspěšné vytvoření nové instance kontaktu.")</span><span class="sxs-lookup"><span data-stu-id="a8345-344">![The browser reflects successful creation of the new contact instance](build-restful-apis-with-aspnet-web-api/_static/image27.png "The browser reflects successful creation of the new contact instance")</span></span>

   <span data-ttu-id="a8345-345">*Prohlížeč odráží úspěšné vytvoření nové instance kontaktu.*</span><span class="sxs-lookup"><span data-stu-id="a8345-345">*The browser reflects successful creation of the new contact instance*</span></span>

> [!NOTE]
> <span data-ttu-id="a8345-346">Kromě toho můžete tuto aplikaci nasadit do Azure podle [dodatku C: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixC).</span><span class="sxs-lookup"><span data-stu-id="a8345-346">Additionally, you can deploy this application to Azure following [Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixC).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="a8345-347">Souhrn</span><span class="sxs-lookup"><span data-stu-id="a8345-347">Summary</span></span>

<span data-ttu-id="a8345-348">Toto testovací prostředí vás zavedlo k novému webovému rozhraní API ASP.NET a implementaci RESTful webových rozhraní API pomocí rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a8345-348">This lab has introduced you to the new ASP.NET Web API framework and to the implementation of RESTful Web APIs using the framework.</span></span> <span data-ttu-id="a8345-349">Z tohoto místa můžete vytvořit nové úložiště, které usnadňuje Trvalost dat pomocí libovolného počtu mechanismů a kabelů, které jsou v tomto testovacím prostředí k dispozici, a nikoli jednoduchého typu.</span><span class="sxs-lookup"><span data-stu-id="a8345-349">From here, you could create a new repository that facilitates data persistence using any number of mechanisms and wire that service up rather than the simple one provided as an example in this lab.</span></span> <span data-ttu-id="a8345-350">Webové rozhraní API podporuje řadu dalších funkcí, například povolení komunikace od klientů, kteří nejsou ve formátu HTML, napsaných v jakémkoli jazyce, který podporuje protokoly HTTP a JSON nebo XML.</span><span class="sxs-lookup"><span data-stu-id="a8345-350">Web API supports a number of additional features, such as enabling communication from non-HTML clients written in any language that supports HTTP and JSON or XML.</span></span> <span data-ttu-id="a8345-351">Možnost hostovat webové rozhraní API mimo typickou webovou aplikaci je také možné, stejně jako možnost vytvářet vlastní formáty serializace.</span><span class="sxs-lookup"><span data-stu-id="a8345-351">The ability to host a Web API outside of a typical web application is also possible, as well as is the ability to create your own serialization formats.</span></span>

<span data-ttu-id="a8345-352">Web ASP.NET má v [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)oblast vyhrazenou pro rozhraní Web API pro ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a8345-352">The ASP.NET Web site has an area dedicated to the ASP.NET Web API framework at [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api).</span></span> <span data-ttu-id="a8345-353">Tato lokalita bude dál poskytovat nejnovější informace, ukázky a novinky související s webovým rozhraním API, proto je pravidelně kontrolovat, pokud byste chtěli vytvořit vlastní webová rozhraní API, která jsou dostupná prakticky pro zařízení nebo vývojové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a8345-353">This site will continue to provide late-breaking information, samples, and news related to Web API, so check it frequently if you'd like to delve deeper into the art of creating custom Web APIs available to virtually any device or development framework.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="a8345-354">Příloha A: používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="a8345-354">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="a8345-355">S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="a8345-355">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="a8345-356">Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="a8345-356">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="a8345-357">![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](build-restful-apis-with-aspnet-web-api/_static/image28.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="a8345-357">![Using Visual Studio code snippets to insert code into your project](build-restful-apis-with-aspnet-web-api/_static/image28.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="a8345-358">*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="a8345-358">*Using Visual Studio code snippets to insert code into your project*</span></span>

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a><span data-ttu-id="a8345-359">Přidání fragmentu kódu pomocí klávesnice (C# pouze)</span><span class="sxs-lookup"><span data-stu-id="a8345-359">To add a code snippet using the keyboard (C# only)</span></span>

1. <span data-ttu-id="a8345-360">Umístěte kurzor na místo, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="a8345-360">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="a8345-361">Začněte psát název fragmentu (bez mezer a spojovníků).</span><span class="sxs-lookup"><span data-stu-id="a8345-361">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="a8345-362">Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="a8345-362">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="a8345-363">Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).</span><span class="sxs-lookup"><span data-stu-id="a8345-363">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="a8345-364">Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="a8345-364">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

    <span data-ttu-id="a8345-365">![Začněte psát název fragmentu.](build-restful-apis-with-aspnet-web-api/_static/image29.png "Začněte psát název fragmentu.")</span><span class="sxs-lookup"><span data-stu-id="a8345-365">![Start typing the snippet name](build-restful-apis-with-aspnet-web-api/_static/image29.png "Start typing the snippet name")</span></span>

    <span data-ttu-id="a8345-366">*Začněte psát název fragmentu.*</span><span class="sxs-lookup"><span data-stu-id="a8345-366">*Start typing the snippet name*</span></span>

    <span data-ttu-id="a8345-367">![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](build-restful-apis-with-aspnet-web-api/_static/image30.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")</span><span class="sxs-lookup"><span data-stu-id="a8345-367">![Press Tab to select the highlighted snippet](build-restful-apis-with-aspnet-web-api/_static/image30.png "Press Tab to select the highlighted snippet")</span></span>

    <span data-ttu-id="a8345-368">*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*</span><span class="sxs-lookup"><span data-stu-id="a8345-368">*Press Tab to select the highlighted snippet*</span></span>

    <span data-ttu-id="a8345-369">![Stiskněte znovu TAB a fragment kódu se rozšíří.](build-restful-apis-with-aspnet-web-api/_static/image31.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")</span><span class="sxs-lookup"><span data-stu-id="a8345-369">![Press Tab again and the snippet will expand](build-restful-apis-with-aspnet-web-api/_static/image31.png "Press Tab again and the snippet will expand")</span></span>

    <span data-ttu-id="a8345-370">*Stiskněte znovu TAB a fragment kódu se rozšíří.*</span><span class="sxs-lookup"><span data-stu-id="a8345-370">*Press Tab again and the snippet will expand*</span></span>

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a><span data-ttu-id="a8345-371">Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)</span><span class="sxs-lookup"><span data-stu-id="a8345-371">To add a code snippet using the mouse (C#, Visual Basic and XML)</span></span>

1. <span data-ttu-id="a8345-372">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="a8345-372">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="a8345-373">Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="a8345-373">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="a8345-374">Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="a8345-374">Pick the relevant snippet from the list, by clicking on it.</span></span>

    <span data-ttu-id="a8345-375">![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](build-restful-apis-with-aspnet-web-api/_static/image32.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")</span><span class="sxs-lookup"><span data-stu-id="a8345-375">![Right-click where you want to insert the code snippet and select Insert Snippet](build-restful-apis-with-aspnet-web-api/_static/image32.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

    <span data-ttu-id="a8345-376">*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*</span><span class="sxs-lookup"><span data-stu-id="a8345-376">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

    <span data-ttu-id="a8345-377">![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](build-restful-apis-with-aspnet-web-api/_static/image33.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")</span><span class="sxs-lookup"><span data-stu-id="a8345-377">![Pick the relevant snippet from the list, by clicking on it](build-restful-apis-with-aspnet-web-api/_static/image33.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

    <span data-ttu-id="a8345-378">*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*</span><span class="sxs-lookup"><span data-stu-id="a8345-378">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="a8345-379">Příloha B: instalace Visual Studio Express 2012 pro web</span><span class="sxs-lookup"><span data-stu-id="a8345-379">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="a8345-380">**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="a8345-380">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="a8345-381">Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="a8345-381">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="a8345-382">Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="a8345-382">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="a8345-383">Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="a8345-383">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="a8345-384">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="a8345-384">Click on **Install Now**.</span></span> <span data-ttu-id="a8345-385">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="a8345-385">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="a8345-386">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="a8345-386">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="a8345-387">![Nainstalovat Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="a8345-387">![Install Visual Studio Express](build-restful-apis-with-aspnet-web-api/_static/image34.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="a8345-388">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="a8345-388">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="a8345-389">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="a8345-389">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí licenčních podmínek](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    <span data-ttu-id="a8345-391">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="a8345-391">*Accepting the license terms*</span></span>
5. <span data-ttu-id="a8345-392">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="a8345-392">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    <span data-ttu-id="a8345-394">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="a8345-394">*Installation progress*</span></span>
6. <span data-ttu-id="a8345-395">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="a8345-395">When the installation completes, click **Finish**.</span></span>

    ![Instalace dokončena](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    <span data-ttu-id="a8345-397">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="a8345-397">*Installation completed*</span></span>
7. <span data-ttu-id="a8345-398">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="a8345-398">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="a8345-399">Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .</span><span class="sxs-lookup"><span data-stu-id="a8345-399">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Dlaždice VS Express for Web](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    <span data-ttu-id="a8345-401">*Dlaždice VS Express for Web*</span><span class="sxs-lookup"><span data-stu-id="a8345-401">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="a8345-402">Příloha C: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="a8345-402">Appendix C: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="a8345-403">V tomto dodatku se dozvíte, jak vytvořit nový web z webu Azure Portal a publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce publikování Nasazení webu, kterou poskytuje Azure.</span><span class="sxs-lookup"><span data-stu-id="a8345-403">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="a8345-404">Úloha 1 – Vytvoření nového webu z webu Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a8345-404">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="a8345-405">Přejít na [portál pro správu Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.</span><span class="sxs-lookup"><span data-stu-id="a8345-405">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8345-406">S Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu.</span><span class="sxs-lookup"><span data-stu-id="a8345-406">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="a8345-407">[Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.</span><span class="sxs-lookup"><span data-stu-id="a8345-407">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="a8345-408">![Přihlaste se k Windows Azure Portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Přihlaste se k Windows Azure Portal")</span><span class="sxs-lookup"><span data-stu-id="a8345-408">![Log on to Windows Azure portal](build-restful-apis-with-aspnet-web-api/_static/image39.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="a8345-409">*Přihlášení k portálu*</span><span class="sxs-lookup"><span data-stu-id="a8345-409">*Log on to Portal*</span></span>
2. <span data-ttu-id="a8345-410">Na panelu příkazů klikněte na **Nový** .</span><span class="sxs-lookup"><span data-stu-id="a8345-410">Click **New** on the command bar.</span></span>

    <span data-ttu-id="a8345-411">![Vytvoření nového webu](build-restful-apis-with-aspnet-web-api/_static/image40.png "Vytvoření nového webu")</span><span class="sxs-lookup"><span data-stu-id="a8345-411">![Creating a new Web Site](build-restful-apis-with-aspnet-web-api/_static/image40.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="a8345-412">*Vytvoření nového webu*</span><span class="sxs-lookup"><span data-stu-id="a8345-412">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="a8345-413">Klikněte na **compute** | **Web**.</span><span class="sxs-lookup"><span data-stu-id="a8345-413">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="a8345-414">Pak vyberte možnost **rychlé vytvoření** .</span><span class="sxs-lookup"><span data-stu-id="a8345-414">Then select **Quick Create** option.</span></span> <span data-ttu-id="a8345-415">Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.</span><span class="sxs-lookup"><span data-stu-id="a8345-415">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8345-416">Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat.</span><span class="sxs-lookup"><span data-stu-id="a8345-416">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="a8345-417">Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do Azure z webu mimo portál.</span><span class="sxs-lookup"><span data-stu-id="a8345-417">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="a8345-418">Nezahrnuje kroky pro nastavení databáze.</span><span class="sxs-lookup"><span data-stu-id="a8345-418">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="a8345-419">![Vytvoření nového webu pomocí rychlého vytvoření](build-restful-apis-with-aspnet-web-api/_static/image41.png "Vytvoření nového webu pomocí rychlého vytvoření")</span><span class="sxs-lookup"><span data-stu-id="a8345-419">![Creating a new Web Site using Quick Create](build-restful-apis-with-aspnet-web-api/_static/image41.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="a8345-420">*Vytvoření nového webu pomocí rychlého vytvoření*</span><span class="sxs-lookup"><span data-stu-id="a8345-420">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="a8345-421">Počkejte, než se nový **Web** vytvoří.</span><span class="sxs-lookup"><span data-stu-id="a8345-421">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="a8345-422">Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** .</span><span class="sxs-lookup"><span data-stu-id="a8345-422">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="a8345-423">Ověřte, zda nový web funguje.</span><span class="sxs-lookup"><span data-stu-id="a8345-423">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="a8345-424">![Procházení na nový web](build-restful-apis-with-aspnet-web-api/_static/image42.png "Procházení na nový web")</span><span class="sxs-lookup"><span data-stu-id="a8345-424">![Browsing to the new web site](build-restful-apis-with-aspnet-web-api/_static/image42.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="a8345-425">*Procházení na nový web*</span><span class="sxs-lookup"><span data-stu-id="a8345-425">*Browsing to the new web site*</span></span>

    <span data-ttu-id="a8345-426">![Běžící Web](build-restful-apis-with-aspnet-web-api/_static/image43.png "Běžící Web")</span><span class="sxs-lookup"><span data-stu-id="a8345-426">![Web site running](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web site running")</span></span>

    <span data-ttu-id="a8345-427">*Běžící Web*</span><span class="sxs-lookup"><span data-stu-id="a8345-427">*Web site running*</span></span>
6. <span data-ttu-id="a8345-428">Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="a8345-428">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="a8345-429">![Otevření stránek správy webu](build-restful-apis-with-aspnet-web-api/_static/image44.png "Otevření stránek správy webu")</span><span class="sxs-lookup"><span data-stu-id="a8345-429">![Opening the web site management pages](build-restful-apis-with-aspnet-web-api/_static/image44.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="a8345-430">*Otevření stránek správy webu*</span><span class="sxs-lookup"><span data-stu-id="a8345-430">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="a8345-431">Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .</span><span class="sxs-lookup"><span data-stu-id="a8345-431">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8345-432">*Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace do Azure pro každou povolenou metodu publikování.</span><span class="sxs-lookup"><span data-stu-id="a8345-432">The *publish profile* contains all of the information required to publish a web application to a Azure for each enabled publication method.</span></span> <span data-ttu-id="a8345-433">Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace.</span><span class="sxs-lookup"><span data-stu-id="a8345-433">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="a8345-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8345-434">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="a8345-435">![Stahuje se publikační profil webu.](build-restful-apis-with-aspnet-web-api/_static/image45.png "Stahuje se publikační profil webu.")</span><span class="sxs-lookup"><span data-stu-id="a8345-435">![Downloading the web site publish profile](build-restful-apis-with-aspnet-web-api/_static/image45.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="a8345-436">*Stahuje se publikační profil webu.*</span><span class="sxs-lookup"><span data-stu-id="a8345-436">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="a8345-437">Stáhněte si soubor profilu publikování do známého umístění.</span><span class="sxs-lookup"><span data-stu-id="a8345-437">Download the publish profile file to a known location.</span></span> <span data-ttu-id="a8345-438">V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace do Azure ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8345-438">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="a8345-439">![Ukládání souboru profilu publikování](build-restful-apis-with-aspnet-web-api/_static/image46.png "Ukládá se publikační profil.")</span><span class="sxs-lookup"><span data-stu-id="a8345-439">![Saving the publish profile file](build-restful-apis-with-aspnet-web-api/_static/image46.png "Saving the publish profile")</span></span>

    <span data-ttu-id="a8345-440">*Ukládání souboru profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="a8345-440">*Saving the publish profile file*</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="a8345-441">Úloha 2 – Konfigurace databázového serveru</span><span class="sxs-lookup"><span data-stu-id="a8345-441">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="a8345-442">Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="a8345-442">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="a8345-443">Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.</span><span class="sxs-lookup"><span data-stu-id="a8345-443">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="a8345-444">Pro uložení aplikační databáze budete potřebovat server SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a8345-444">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="a8345-445">SQL Database servery můžete zobrazit z předplatného na portálu pro správu Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**.</span><span class="sxs-lookup"><span data-stu-id="a8345-445">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="a8345-446">Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="a8345-446">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="a8345-447">Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách.</span><span class="sxs-lookup"><span data-stu-id="a8345-447">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="a8345-448">Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.</span><span class="sxs-lookup"><span data-stu-id="a8345-448">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="a8345-449">![Řídicí panel serveru SQL Database](build-restful-apis-with-aspnet-web-api/_static/image47.png "Řídicí panel serveru SQL Database")</span><span class="sxs-lookup"><span data-stu-id="a8345-449">![SQL Database Server Dashboard](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="a8345-450">*Řídicí panel serveru SQL Database*</span><span class="sxs-lookup"><span data-stu-id="a8345-450">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="a8345-451">V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru.</span><span class="sxs-lookup"><span data-stu-id="a8345-451">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="a8345-452">Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](build-restful-apis-with-aspnet-web-api/_static/image48.png).</span><span class="sxs-lookup"><span data-stu-id="a8345-452">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) button.</span></span>

    ![Přidává se IP adresa klienta.](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    <span data-ttu-id="a8345-454">*Přidává se IP adresa klienta.*</span><span class="sxs-lookup"><span data-stu-id="a8345-454">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="a8345-455">Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="a8345-455">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Potvrdit změny](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    <span data-ttu-id="a8345-457">*Potvrdit změny*</span><span class="sxs-lookup"><span data-stu-id="a8345-457">*Confirm Changes*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="a8345-458">Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu</span><span class="sxs-lookup"><span data-stu-id="a8345-458">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="a8345-459">Vraťte se do řešení ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="a8345-459">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="a8345-460">V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="a8345-460">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="a8345-461">![Publikování aplikace](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publikování aplikace")</span><span class="sxs-lookup"><span data-stu-id="a8345-461">![Publishing the Application](build-restful-apis-with-aspnet-web-api/_static/image51.png "Publishing the Application")</span></span>

    <span data-ttu-id="a8345-462">*Publikování webu*</span><span class="sxs-lookup"><span data-stu-id="a8345-462">*Publishing the web site*</span></span>
2. <span data-ttu-id="a8345-463">Importujte profil publikování, který jste uložili v prvním úkolu.</span><span class="sxs-lookup"><span data-stu-id="a8345-463">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="a8345-464">![Import profilu publikování](build-restful-apis-with-aspnet-web-api/_static/image52.png "Import profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="a8345-464">![Importing the publish profile](build-restful-apis-with-aspnet-web-api/_static/image52.png "Importing the publish profile")</span></span>

    <span data-ttu-id="a8345-465">*Importuje se publikační profil.*</span><span class="sxs-lookup"><span data-stu-id="a8345-465">*Importing publish profile*</span></span>
3. <span data-ttu-id="a8345-466">Klikněte na **ověřit připojení**.</span><span class="sxs-lookup"><span data-stu-id="a8345-466">Click **Validate Connection**.</span></span> <span data-ttu-id="a8345-467">Po dokončení ověřování klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="a8345-467">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8345-468">Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.</span><span class="sxs-lookup"><span data-stu-id="a8345-468">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="a8345-469">![Ověřování připojení](build-restful-apis-with-aspnet-web-api/_static/image53.png "Ověřování připojení")</span><span class="sxs-lookup"><span data-stu-id="a8345-469">![Validating connection](build-restful-apis-with-aspnet-web-api/_static/image53.png "Validating connection")</span></span>

    <span data-ttu-id="a8345-470">*Ověřování připojení*</span><span class="sxs-lookup"><span data-stu-id="a8345-470">*Validating connection*</span></span>
4. <span data-ttu-id="a8345-471">Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="a8345-471">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="a8345-472">![Konfigurace nasazení webu](build-restful-apis-with-aspnet-web-api/_static/image54.png "Konfigurace nasazení webu")</span><span class="sxs-lookup"><span data-stu-id="a8345-472">![Web deploy configuration](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web deploy configuration")</span></span>

    <span data-ttu-id="a8345-473">*Konfigurace nasazení webu*</span><span class="sxs-lookup"><span data-stu-id="a8345-473">*Web deploy configuration*</span></span>
5. <span data-ttu-id="a8345-474">Připojení k databázi nakonfigurujte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a8345-474">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="a8345-475">Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .</span><span class="sxs-lookup"><span data-stu-id="a8345-475">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="a8345-476">V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="a8345-476">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="a8345-477">V **heslo** zadejte přihlašovací heslo správce serveru.</span><span class="sxs-lookup"><span data-stu-id="a8345-477">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="a8345-478">Zadejte nový název databáze, například: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="a8345-478">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="a8345-479">![Konfigurace cílového připojovacího řetězce](build-restful-apis-with-aspnet-web-api/_static/image55.png "Konfigurace cílového připojovacího řetězce")</span><span class="sxs-lookup"><span data-stu-id="a8345-479">![Configuring destination connection string](build-restful-apis-with-aspnet-web-api/_static/image55.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="a8345-480">*Konfigurace cílového připojovacího řetězce*</span><span class="sxs-lookup"><span data-stu-id="a8345-480">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="a8345-481">Pak klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8345-481">Then click **OK**.</span></span> <span data-ttu-id="a8345-482">Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="a8345-482">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="a8345-483">![Vytvoření databáze](build-restful-apis-with-aspnet-web-api/_static/image56.png "Vytváří se řetězec databáze.")</span><span class="sxs-lookup"><span data-stu-id="a8345-483">![Creating the database](build-restful-apis-with-aspnet-web-api/_static/image56.png "Creating the database string")</span></span>

    <span data-ttu-id="a8345-484">*Vytvoření databáze*</span><span class="sxs-lookup"><span data-stu-id="a8345-484">*Creating the database*</span></span>
7. <span data-ttu-id="a8345-485">Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení.</span><span class="sxs-lookup"><span data-stu-id="a8345-485">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="a8345-486">Pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="a8345-486">Then click **Next**.</span></span>

    <span data-ttu-id="a8345-487">![Připojovací řetězec ukazující na SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Připojovací řetězec ukazující na SQL Database")</span><span class="sxs-lookup"><span data-stu-id="a8345-487">![Connection string pointing to SQL Database](build-restful-apis-with-aspnet-web-api/_static/image57.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="a8345-488">*Připojovací řetězec ukazující na SQL Database*</span><span class="sxs-lookup"><span data-stu-id="a8345-488">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="a8345-489">Na stránce **Náhled** klikněte na **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="a8345-489">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="a8345-490">![Publikování webové aplikace](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publikování webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="a8345-490">![Publishing the web application](build-restful-apis-with-aspnet-web-api/_static/image58.png "Publishing the web application")</span></span>

    <span data-ttu-id="a8345-491">*Publikování webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="a8345-491">*Publishing the web application*</span></span>
9. <span data-ttu-id="a8345-492">Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.</span><span class="sxs-lookup"><span data-stu-id="a8345-492">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="a8345-493">![Aplikace byla publikována na platformě Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Aplikace byla publikována na platformě Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="a8345-493">![Application published to Windows Azure](build-restful-apis-with-aspnet-web-api/_static/image59.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="a8345-494">*Aplikace byla publikována do Azure*</span><span class="sxs-lookup"><span data-stu-id="a8345-494">*Application published to Azure*</span></span>
