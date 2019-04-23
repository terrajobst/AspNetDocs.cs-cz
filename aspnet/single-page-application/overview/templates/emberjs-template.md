---
uid: single-page-application/overview/templates/emberjs-template
title: Šablona emberjs | Dokumentace Microsoftu
author: xqiu
description: Šablona EmberJS
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: e2bb8a13a0036f1fcfdcfd03a6a6e74e886a7f2c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59406857"
---
# <a name="emberjs-template"></a><span data-ttu-id="18655-103">Šablona EmberJS</span><span class="sxs-lookup"><span data-stu-id="18655-103">EmberJS template</span></span>

<span data-ttu-id="18655-104">podle [Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="18655-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="18655-105">Šablona Emberjs MVC je vytvořená systémem Nathan Totten Thiago Santos a Xinyang Qiu.</span><span class="sxs-lookup"><span data-stu-id="18655-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="18655-106">Stažení šablony EmberJS MVC</span><span class="sxs-lookup"><span data-stu-id="18655-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)


<span data-ttu-id="18655-107">Šablona EmberJS SPA je určena vám pomůžou začít rychle vytvářet interaktivní webové klientské aplikace s využitím EmberJS.</span><span class="sxs-lookup"><span data-stu-id="18655-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="18655-108">"Jednostránková aplikace" (SPA) je obecný termín pro webovou aplikaci, která načte jednu stránku HTML a následně aktualizuje dynamicky, místo načtení nové stránky na stránku.</span><span class="sxs-lookup"><span data-stu-id="18655-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="18655-109">Po načtení počáteční stránky tato jednostránková aplikace komunikuje se serverem přes odesílání požadavků AJAX.</span><span class="sxs-lookup"><span data-stu-id="18655-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="18655-110">AJAX není nic nového, ale ještě dnes existují architektury JavaScriptu, které usnadňují tvorbu a udržování rozsáhlé sofistikované aplikace SPA.</span><span class="sxs-lookup"><span data-stu-id="18655-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="18655-111">Navíc HTML 5 a CSS3 jsou to usnadňuje vytváření bohatých uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="18655-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="18655-112">Používá šablona Emberjs SPA [členskými](http://emberjs.com/) JavaScript library pro zpracování aktualizace stránky AJAX požadavků.</span><span class="sxs-lookup"><span data-stu-id="18655-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="18655-113">Ember.js používá datové vazby k synchronizaci na stránce s nejnovější data.</span><span class="sxs-lookup"><span data-stu-id="18655-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="18655-114">Tímto způsobem nemusíte psát žádný kód, který vás provede JSON data a aktualizace modelu DOM.</span><span class="sxs-lookup"><span data-stu-id="18655-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="18655-115">Místo toho kam si ukládáte deklarativních atributů ve formátu HTML, který Ember.js instrukce, jak data můžete prezentovat tak.</span><span class="sxs-lookup"><span data-stu-id="18655-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="18655-116">Na straně serveru, je téměř stejný jako šablona emberjs [šablona KnockoutJS SPA](../introduction/knockoutjs-template.md).</span><span class="sxs-lookup"><span data-stu-id="18655-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="18655-117">ASP.NET MVC používá k poskytování dokumentů HTML a ASP.NET Web API pro zpracování požadavků AJAX od klienta.</span><span class="sxs-lookup"><span data-stu-id="18655-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="18655-118">Další informace o tyto aspekty šablony [šablona KnockoutJS](../introduction/knockoutjs-template.md) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="18655-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="18655-119">Toto téma se zaměřuje na rozdíly mezi šablony Knockout a šablona emberjs.</span><span class="sxs-lookup"><span data-stu-id="18655-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="18655-120">Vytvoření projektu šablona EmberJS SPA</span><span class="sxs-lookup"><span data-stu-id="18655-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="18655-121">Stáhněte a nainstalujte šablony kliknutím na tlačítko Stáhnout výše.</span><span class="sxs-lookup"><span data-stu-id="18655-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="18655-122">Můžete potřebovat restartovat Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="18655-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="18655-123">V **šablony** vyberte **nainstalované šablony** a rozbalte **Visual C#** uzlu.</span><span class="sxs-lookup"><span data-stu-id="18655-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="18655-124">V části **Visual C#** vyberte **webové**.</span><span class="sxs-lookup"><span data-stu-id="18655-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="18655-125">V seznamu šablon projektu vyberte **webové aplikace ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="18655-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="18655-126">Pojmenujte projekt a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="18655-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="18655-127">V **nový projekt** průvodce, vyberte **Ember.js SPA projektu**.</span><span class="sxs-lookup"><span data-stu-id="18655-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="18655-128">Přehled šablon SPA EmberJS</span><span class="sxs-lookup"><span data-stu-id="18655-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="18655-129">Šablona emberjs používá kombinaci jQuery, Ember.js, Handlebars.js vytvořit plynulé a na interaktivní uživatelské rozhraní.</span><span class="sxs-lookup"><span data-stu-id="18655-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="18655-130">Ember.js je knihovna jazyka JavaScript, která používá vzor MVC na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="18655-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="18655-131">A *šablony*napsaných v jazyce šablonování Handlebars, popisuje uživatelské rozhraní aplikace.</span><span class="sxs-lookup"><span data-stu-id="18655-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="18655-132">V režimu vydání [Handlebars kompilátoru](https://github.com/Myslik/csharp-ember-handlebars) slouží k vytvoření balíčku a kompilaci handlebars šablony.</span><span class="sxs-lookup"><span data-stu-id="18655-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="18655-133">A *modelu* ukládá data aplikací, který získá ze serveru (ToDo seznamy a položky seznamu úkolů).</span><span class="sxs-lookup"><span data-stu-id="18655-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="18655-134">A *řadič* uloží stav aplikace.</span><span class="sxs-lookup"><span data-stu-id="18655-134">A *controller* stores application state.</span></span> <span data-ttu-id="18655-135">Kontrolery často prezentovat data modelu na odpovídající šablony.</span><span class="sxs-lookup"><span data-stu-id="18655-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="18655-136">A *zobrazení* přeloží primitivní události z aplikace a předává do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="18655-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="18655-137">A *směrovače* spravuje stav aplikace, udržování synchronizace šablony a adresy URL.</span><span class="sxs-lookup"><span data-stu-id="18655-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="18655-138">Kromě toho knihovna členskými dat je možné synchronizovat objekty JSON (získané ze serveru prostřednictvím rozhraní RESTful API) a modely klienta.</span><span class="sxs-lookup"><span data-stu-id="18655-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="18655-139">Šablona EmberJS SPA slouží k uspořádání skripty do osm vrstvy:</span><span class="sxs-lookup"><span data-stu-id="18655-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="18655-140">webapi\_adapter.js, webapi\_serializer.js: Rozšiřuje knihovna členskými dat pro práci s rozhraním ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="18655-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="18655-141">Scripts/helpers.js: Definuje nový členskými Handlebars pomocné rutiny.</span><span class="sxs-lookup"><span data-stu-id="18655-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="18655-142">Scripts/app.js: Vytvoří aplikaci a nakonfiguruje adaptéru a serializátor.</span><span class="sxs-lookup"><span data-stu-id="18655-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="18655-143">Scripts/app/models/\*.js: Definuje modely.</span><span class="sxs-lookup"><span data-stu-id="18655-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="18655-144">Skripty aaplikace/zobrazení/\*js: Definuje zobrazení.</span><span class="sxs-lookup"><span data-stu-id="18655-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="18655-145">Scripts/app/controllers/\*.js: Definuje řadiče.</span><span class="sxs-lookup"><span data-stu-id="18655-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="18655-146">Skripty/aplikace/trasy, Scripts/app/router.js: Definuje trasy.</span><span class="sxs-lookup"><span data-stu-id="18655-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="18655-147">Šablony /\*.hbs: Definuje handlebars šablony.</span><span class="sxs-lookup"><span data-stu-id="18655-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="18655-148">Pojďme se podívat na některé z těchto skriptů podrobněji.</span><span class="sxs-lookup"><span data-stu-id="18655-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="18655-149">Modely</span><span class="sxs-lookup"><span data-stu-id="18655-149">Models</span></span>

<span data-ttu-id="18655-150">Tyto modely jsou definovány ve složce skripty/aplikace/modely.</span><span class="sxs-lookup"><span data-stu-id="18655-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="18655-151">Existují dva soubory modelu: todoItem.js a todoList.js.</span><span class="sxs-lookup"><span data-stu-id="18655-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="18655-152">**TODO.model.js** definuje modely (prohlížeč) na straně klienta pro seznamy úkolů.</span><span class="sxs-lookup"><span data-stu-id="18655-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="18655-153">Existují dvě třídy modelu: todoItem a seznamu úkolů.</span><span class="sxs-lookup"><span data-stu-id="18655-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="18655-154">V členskými modely jsou podtřídami DS. Model.</span><span class="sxs-lookup"><span data-stu-id="18655-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="18655-155">Model může mít vlastnosti s atributy:</span><span class="sxs-lookup"><span data-stu-id="18655-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="18655-156">Modely lze definovat vztahy s jinými modely:</span><span class="sxs-lookup"><span data-stu-id="18655-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="18655-157">Modely můžou mít vypočítané vlastnosti, kteří jsou navázáni na další vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="18655-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="18655-158">Modely mohou být pozorovatel funkce, které jsou vyvolány při změně zjištěné vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="18655-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="18655-159">Zobrazení</span><span class="sxs-lookup"><span data-stu-id="18655-159">Views</span></span>

<span data-ttu-id="18655-160">Zobrazení jsou definovány ve složce skripty/aplikace/zobrazení.</span><span class="sxs-lookup"><span data-stu-id="18655-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="18655-161">Zobrazení přeloží události z uživatelského rozhraní aplikace.</span><span class="sxs-lookup"><span data-stu-id="18655-161">A view translates events from the application UI.</span></span> <span data-ttu-id="18655-162">Obslužné rutiny události můžete zpětné volání pro kontroler funkce nebo jednoduše datového kontextu volat přímo.</span><span class="sxs-lookup"><span data-stu-id="18655-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="18655-163">Například následující kód je z views/TodoItemEditView.js.</span><span class="sxs-lookup"><span data-stu-id="18655-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="18655-164">Definuje události u vstupního textového pole.</span><span class="sxs-lookup"><span data-stu-id="18655-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="18655-165">Kontroler</span><span class="sxs-lookup"><span data-stu-id="18655-165">Controller</span></span>

<span data-ttu-id="18655-166">Kontrolery jsou definovány ve složce skripty/aplikace/řadiče.</span><span class="sxs-lookup"><span data-stu-id="18655-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="18655-167">K reprezentaci jednoho modelu rozšíření `Ember.ObjectController`:</span><span class="sxs-lookup"><span data-stu-id="18655-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="18655-168">Kontroler může také představovat kolekce modelů rozšířením `Ember.ArrayController`.</span><span class="sxs-lookup"><span data-stu-id="18655-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="18655-169">Například, TodoListController reprezentuje pole prvků `todoList` objekty.</span><span class="sxs-lookup"><span data-stu-id="18655-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="18655-170">Kontroler se seřadí podle ID seznamu úkolů v sestupném pořadí:</span><span class="sxs-lookup"><span data-stu-id="18655-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="18655-171">Kontroler definuje funkci nazvanou `addTodoList`, který vytvoří nový seznam úkolů a přidá jej do pole.</span><span class="sxs-lookup"><span data-stu-id="18655-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="18655-172">Pokud chcete zobrazit, jak tato funkce volána, otevřete soubor šablony s názvem todoListTemplate.html do složky šablony.</span><span class="sxs-lookup"><span data-stu-id="18655-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="18655-173">Následující kód šablony vytvoří vazbu na tlačítko `addTodoList` funkce:</span><span class="sxs-lookup"><span data-stu-id="18655-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="18655-174">Také obsahuje kontroler `error` vlastnost, která obsahuje chybovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="18655-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="18655-175">Tady je kód šablony zobrazíte chybovou zprávu (také v todoListTemplate.html):</span><span class="sxs-lookup"><span data-stu-id="18655-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="18655-176">Trasy</span><span class="sxs-lookup"><span data-stu-id="18655-176">Routes</span></span>

<span data-ttu-id="18655-177">Router.js trasy a výchozí šablonu pro zobrazení, nastaví stav aplikace, definuje a odpovídá adresy URL trasy:</span><span class="sxs-lookup"><span data-stu-id="18655-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="18655-178">TodoListRoute.js načte data pro TodoListRoute tak, že přepíšete setupController funkce:</span><span class="sxs-lookup"><span data-stu-id="18655-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="18655-179">Členskými používá konvence pojmenování k přiřazení adres URL, názvy tras, kontrolerů a šablony.</span><span class="sxs-lookup"><span data-stu-id="18655-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="18655-180">Další informace najdete v tématu [ http://emberjs.com/guides/routing/defining-your-routes/ ](http://emberjs.com/guides/routing/defining-your-routes/) v dokumentaci EmberJS.</span><span class="sxs-lookup"><span data-stu-id="18655-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="18655-181">Šablony</span><span class="sxs-lookup"><span data-stu-id="18655-181">Templates</span></span>

<span data-ttu-id="18655-182">Složka šablony obsahuje čtyři šablony:</span><span class="sxs-lookup"><span data-stu-id="18655-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="18655-183">application.hbs: Výchozí šablony, který je vykreslen při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="18655-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="18655-184">about.hbs: Šablona trasy "/ o".</span><span class="sxs-lookup"><span data-stu-id="18655-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="18655-185">index.hbs: Šablona pro kořenovou trasy "/".</span><span class="sxs-lookup"><span data-stu-id="18655-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="18655-186">todoList.hbs: Šablona pro "/ todo" trasy.</span><span class="sxs-lookup"><span data-stu-id="18655-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="18655-187">\_navbar.hbs: Šablona definuje navigační nabídky.</span><span class="sxs-lookup"><span data-stu-id="18655-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="18655-188">Šablona aplikace funguje jako hlavní stránky.</span><span class="sxs-lookup"><span data-stu-id="18655-188">The application template acts like a master page.</span></span> <span data-ttu-id="18655-189">Obsahuje záhlaví, zápatí nebo "{{zásuvky}}" Vložit další šablony v v závislosti na trasy.</span><span class="sxs-lookup"><span data-stu-id="18655-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="18655-190">Další informace o šablonách aplikací v členskými najdete v tématu [ http://guides.emberjs.com/v1.10.0/templates/the-application-template// ](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span><span class="sxs-lookup"><span data-stu-id="18655-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="18655-191">"/ Seznam úkolů" Šablona obsahuje dvou výrazů smyčky.</span><span class="sxs-lookup"><span data-stu-id="18655-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="18655-192">Vnější smyčka je `{{#each controller}}`a uvnitř smyčka je `{{#each todos}}`.</span><span class="sxs-lookup"><span data-stu-id="18655-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="18655-193">Následující kód ukazuje vestavěná `Ember.Checkbox` zobrazíte přizpůsobený `App.TodoItemEditView`a odkaz s `deleteTodo` akce.</span><span class="sxs-lookup"><span data-stu-id="18655-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="18655-194">`HtmlHelperExtensions` Třídy definované v Controllers/HtmlHelperExtensions.cs, definuje pomocnou rutinu funkce do mezipaměti a Vložit šablonu souborů při **ladění** je nastavena na **true** v souboru Web.config.</span><span class="sxs-lookup"><span data-stu-id="18655-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExtensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="18655-195">Tato funkce je volána z definované v Views/Home/App.cshtml soubor zobrazení ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="18655-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="18655-196">Volat bez argumentů, vykreslí funkci všechny soubory šablon do složky šablony.</span><span class="sxs-lookup"><span data-stu-id="18655-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="18655-197">Můžete také zadat podsložku nebo soubor konkrétní šablony.</span><span class="sxs-lookup"><span data-stu-id="18655-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="18655-198">Když **ladění** je **false** v souboru Web.config, aplikace obsahuje položku sady "~/bundles/templates".</span><span class="sxs-lookup"><span data-stu-id="18655-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="18655-199">Tato položka sady přidá BundleConfig.cs pomocí knihovny kompilátoru Handlebars:</span><span class="sxs-lookup"><span data-stu-id="18655-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
