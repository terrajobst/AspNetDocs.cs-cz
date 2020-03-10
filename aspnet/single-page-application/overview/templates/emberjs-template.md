---
uid: single-page-application/overview/templates/emberjs-template
title: Šablona EmberJS | Microsoft Docs
author: xqiu
description: Šablona EmberJS
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578503"
---
# <a name="emberjs-template"></a><span data-ttu-id="71832-103">Šablona EmberJS</span><span class="sxs-lookup"><span data-stu-id="71832-103">EmberJS template</span></span>

<span data-ttu-id="71832-104">od [Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="71832-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="71832-105">Šablona EmberJS MVC je zapsána Nathan Totten, Thiago Santos a Xinyang Qiu.</span><span class="sxs-lookup"><span data-stu-id="71832-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="71832-106">Stažení šablony EmberJS MVC</span><span class="sxs-lookup"><span data-stu-id="71832-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)

<span data-ttu-id="71832-107">Šablona EmberJS SPA je navržená tak, aby vám mohla rychle začít vytvářet interaktivní webové aplikace na straně klienta pomocí EmberJS.</span><span class="sxs-lookup"><span data-stu-id="71832-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="71832-108">Jednostránkové aplikace (SPA) je obecný termín pro webovou aplikaci, která načte jednu stránku HTML a pak dynamicky aktualizuje stránku místo načtení nových stránek.</span><span class="sxs-lookup"><span data-stu-id="71832-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="71832-109">Po počátečním načtení stránky mluví zabezpečené připojení k serveru přes požadavky AJAX.</span><span class="sxs-lookup"><span data-stu-id="71832-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="71832-110">AJAX není nic nového, ale dnes existuje rozhraní JavaScript, které usnadňuje sestavování a údržbu rozsáhlých propracovaných aplikací s SPA.</span><span class="sxs-lookup"><span data-stu-id="71832-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="71832-111">Také HTML 5 a CSS3 usnadňují vytváření bohatých uživatelská rozhraní.</span><span class="sxs-lookup"><span data-stu-id="71832-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="71832-112">Šablona EmberJS SPA používá knihovnu JavaScript [života](http://emberjs.com/) ke zpracování aktualizací stránky od požadavků AJAX.</span><span class="sxs-lookup"><span data-stu-id="71832-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="71832-113">Života. js používá datovou vazbu k synchronizaci stránky s nejnovějšími daty.</span><span class="sxs-lookup"><span data-stu-id="71832-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="71832-114">Tímto způsobem nemusíte psát žádný kód, který projde daty JSON a aktualizuje DOM.</span><span class="sxs-lookup"><span data-stu-id="71832-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="71832-115">Místo toho umístíte deklarativní atributy do kódu HTML, které sděluje života. js, jak prezentovat data.</span><span class="sxs-lookup"><span data-stu-id="71832-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="71832-116">Na straně serveru je šablona EmberJS skoro shodná se [šablonou KNOCKOUTJS Spa](../introduction/knockoutjs-template.md).</span><span class="sxs-lookup"><span data-stu-id="71832-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="71832-117">Používá ASP.NET MVC k poskytování dokumentů HTML a webové rozhraní API ASP.NET pro zpracování požadavků AJAX od klienta.</span><span class="sxs-lookup"><span data-stu-id="71832-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="71832-118">Další informace o těchto aspektech šablony najdete v dokumentaci k [šabloně KnockoutJS](../introduction/knockoutjs-template.md) .</span><span class="sxs-lookup"><span data-stu-id="71832-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="71832-119">Toto téma se zaměřuje na rozdíly mezi šablonou vyseknutí a šablonou EmberJS.</span><span class="sxs-lookup"><span data-stu-id="71832-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="71832-120">Vytvoření projektu šablony EmberJS SPA</span><span class="sxs-lookup"><span data-stu-id="71832-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="71832-121">Stáhněte a nainstalujte šablonu kliknutím na tlačítko Stáhnout výše.</span><span class="sxs-lookup"><span data-stu-id="71832-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="71832-122">Možná budete muset restartovat Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71832-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="71832-123">V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** .</span><span class="sxs-lookup"><span data-stu-id="71832-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="71832-124">V **části C#vizuál** vyberte **Web**.</span><span class="sxs-lookup"><span data-stu-id="71832-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="71832-125">V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="71832-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="71832-126">Pojmenujte projekt a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="71832-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="71832-127">V průvodci **vytvořením nového projektu** vyberte **projekt života. js Spa**.</span><span class="sxs-lookup"><span data-stu-id="71832-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="71832-128">Přehled šablony EmberJS SPA</span><span class="sxs-lookup"><span data-stu-id="71832-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="71832-129">Šablona EmberJS používá kombinaci jQuery, života. js, handlebars. js k vytvoření hladkého interaktivního uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="71832-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="71832-130">Života. js je knihovna JavaScriptu, která používá model MVC na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="71832-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="71832-131">*Šablona*napsaná v jazyce handlebars šablonování popisuje uživatelské rozhraní aplikace.</span><span class="sxs-lookup"><span data-stu-id="71832-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="71832-132">V režimu vydání se [kompilátor handlebars](https://github.com/Myslik/csharp-ember-handlebars) používá k vytvoření balíčku a zkompilování šablony handlebars.</span><span class="sxs-lookup"><span data-stu-id="71832-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="71832-133">*Model* ukládá data aplikace, která získá ze serveru (seznamy úkolů a položky ToDo).</span><span class="sxs-lookup"><span data-stu-id="71832-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="71832-134">*Kontrolér* ukládá stav aplikace.</span><span class="sxs-lookup"><span data-stu-id="71832-134">A *controller* stores application state.</span></span> <span data-ttu-id="71832-135">Řadiče často prezentují data modelu do odpovídajících šablon.</span><span class="sxs-lookup"><span data-stu-id="71832-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="71832-136">*Zobrazení* překládá primitivní události z aplikace a předá je řadiči.</span><span class="sxs-lookup"><span data-stu-id="71832-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="71832-137">*Směrovač* spravuje stav aplikace a udržuje synchronizaci adres URL a šablon.</span><span class="sxs-lookup"><span data-stu-id="71832-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="71832-138">Kromě toho je možné pomocí knihovny dat života synchronizovat objekty JSON (získané ze serveru prostřednictvím rozhraní RESTful API) a modely klientů.</span><span class="sxs-lookup"><span data-stu-id="71832-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="71832-139">Šablona EmberJS SPA uspořádá skripty do osmi vrstev:</span><span class="sxs-lookup"><span data-stu-id="71832-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="71832-140">WebApi\_Adapter. js, WebApi\_serializátor. js: rozšiřuje knihovnu dat života pro práci s webovým rozhraním API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="71832-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="71832-141">Skripty/pomocníky. js: definuje nové Handlebarsy pomocníka pro života.</span><span class="sxs-lookup"><span data-stu-id="71832-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="71832-142">Skripty/App. js: Vytvoří aplikaci a nakonfiguruje adaptér a serializátor.</span><span class="sxs-lookup"><span data-stu-id="71832-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="71832-143">Skripty/aplikace/modely/\*. js: definuje modely.</span><span class="sxs-lookup"><span data-stu-id="71832-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="71832-144">Skripty/aplikace/zobrazení/\*. js: definuje zobrazení.</span><span class="sxs-lookup"><span data-stu-id="71832-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="71832-145">Skripty/aplikace/řadiče/\*. js: definuje řadiče.</span><span class="sxs-lookup"><span data-stu-id="71832-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="71832-146">Skripty, aplikace/trasy, skripty/aplikace/směrovač. js: definuje trasy.</span><span class="sxs-lookup"><span data-stu-id="71832-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="71832-147">Templates/\*. hr: definuje šablony handlebars.</span><span class="sxs-lookup"><span data-stu-id="71832-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="71832-148">Pojďme se podívat na některé z těchto skriptů podrobněji.</span><span class="sxs-lookup"><span data-stu-id="71832-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="71832-149">Modely</span><span class="sxs-lookup"><span data-stu-id="71832-149">Models</span></span>

<span data-ttu-id="71832-150">Modely jsou definovány ve složce Scripts/app/modely.</span><span class="sxs-lookup"><span data-stu-id="71832-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="71832-151">Existují dva soubory modelů: todoItem. js a todoList. js.</span><span class="sxs-lookup"><span data-stu-id="71832-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="71832-152">**todo. model. js** definuje modely na straně klienta (prohlížeč) pro seznamy úkolů.</span><span class="sxs-lookup"><span data-stu-id="71832-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="71832-153">Existují dvě třídy modelů: todoItem a todoList.</span><span class="sxs-lookup"><span data-stu-id="71832-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="71832-154">V života jsou modely podtřídy DS. Vzorový.</span><span class="sxs-lookup"><span data-stu-id="71832-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="71832-155">Model může mít vlastnosti s atributy:</span><span class="sxs-lookup"><span data-stu-id="71832-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="71832-156">Modely můžou definovat relace s jinými modely:</span><span class="sxs-lookup"><span data-stu-id="71832-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="71832-157">Modely mohou mít vypočítané vlastnosti, které se vážou na jiné vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="71832-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="71832-158">Modely mohou mít funkce pozorovatele, které jsou vyvolány při změně pozorované vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="71832-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="71832-159">Zobrazení</span><span class="sxs-lookup"><span data-stu-id="71832-159">Views</span></span>

<span data-ttu-id="71832-160">Zobrazení jsou definována ve složce Scripts/app/views.</span><span class="sxs-lookup"><span data-stu-id="71832-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="71832-161">Zobrazení překládá události z uživatelského rozhraní aplikace.</span><span class="sxs-lookup"><span data-stu-id="71832-161">A view translates events from the application UI.</span></span> <span data-ttu-id="71832-162">Obslužná rutina události může volat zpět do funkcí kontroleru nebo jednoduše volat kontext dat přímo.</span><span class="sxs-lookup"><span data-stu-id="71832-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="71832-163">Například následující kód je ze zobrazení/TodoItemEditView. js.</span><span class="sxs-lookup"><span data-stu-id="71832-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="71832-164">Definuje zpracování událostí pro vstupní textové pole.</span><span class="sxs-lookup"><span data-stu-id="71832-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="71832-165">Kontrolér</span><span class="sxs-lookup"><span data-stu-id="71832-165">Controller</span></span>

<span data-ttu-id="71832-166">Řadiče se definují ve složce Scripts/App/Controllers.</span><span class="sxs-lookup"><span data-stu-id="71832-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="71832-167">Chcete-li reprezentovat jeden model, rozšíří `Ember.ObjectController`:</span><span class="sxs-lookup"><span data-stu-id="71832-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="71832-168">Kontroler může také představovat kolekci modelů rozšířením `Ember.ArrayController`.</span><span class="sxs-lookup"><span data-stu-id="71832-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="71832-169">Například TodoListController představuje pole objektů `todoList`.</span><span class="sxs-lookup"><span data-stu-id="71832-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="71832-170">Kontroler seřadí podle ID todoList v sestupném pořadí:</span><span class="sxs-lookup"><span data-stu-id="71832-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="71832-171">Kontroler definuje funkci s názvem `addTodoList`, která vytvoří novou todoList a přidá ji do pole.</span><span class="sxs-lookup"><span data-stu-id="71832-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="71832-172">Chcete-li zjistit, jakým způsobem bude tato funkce volána, otevřete soubor šablony s názvem todoListTemplate. html ve složce šablony.</span><span class="sxs-lookup"><span data-stu-id="71832-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="71832-173">Následující kód šablony váže tlačítko k funkci `addTodoList`:</span><span class="sxs-lookup"><span data-stu-id="71832-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="71832-174">Kontroler obsahuje také vlastnost `error`, která obsahuje chybovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="71832-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="71832-175">Zde je kód šablony pro zobrazení chybové zprávy (také v souboru todoListTemplate. html):</span><span class="sxs-lookup"><span data-stu-id="71832-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="71832-176">Trasy</span><span class="sxs-lookup"><span data-stu-id="71832-176">Routes</span></span>

<span data-ttu-id="71832-177">Směrovač. js definuje trasy a výchozí šablonu pro zobrazení, nastavení stavu aplikace a odpovídá adresám URL na trasy:</span><span class="sxs-lookup"><span data-stu-id="71832-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="71832-178">TodoListRoute. js načte data pro TodoListRoute přepsáním funkce setupController:</span><span class="sxs-lookup"><span data-stu-id="71832-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="71832-179">Života používá konvence pojmenování, které odpovídají adresám URL, názvům tras, řadičům a šablonám.</span><span class="sxs-lookup"><span data-stu-id="71832-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="71832-180">Další informace najdete v tématu [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) v dokumentaci k EmberJS.</span><span class="sxs-lookup"><span data-stu-id="71832-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="71832-181">Šablony</span><span class="sxs-lookup"><span data-stu-id="71832-181">Templates</span></span>

<span data-ttu-id="71832-182">Složka šablony obsahuje čtyři šablony:</span><span class="sxs-lookup"><span data-stu-id="71832-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="71832-183">Application. hr: výchozí šablona, která je vykreslena při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="71832-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="71832-184">o. hr: Šablona pro trasu "/About".</span><span class="sxs-lookup"><span data-stu-id="71832-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="71832-185">index. hr: Šablona pro kořenovou trasu "/".</span><span class="sxs-lookup"><span data-stu-id="71832-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="71832-186">todoList. hr: Šablona pro trasu "/todo".</span><span class="sxs-lookup"><span data-stu-id="71832-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="71832-187">\_panel. hr: Šablona definuje navigační nabídku.</span><span class="sxs-lookup"><span data-stu-id="71832-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="71832-188">Šablona aplikace funguje jako stránka předlohy.</span><span class="sxs-lookup"><span data-stu-id="71832-188">The application template acts like a master page.</span></span> <span data-ttu-id="71832-189">Obsahuje záhlaví, zápatí a "{{vývod}}" pro vložení dalších šablon v závislosti na trase.</span><span class="sxs-lookup"><span data-stu-id="71832-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="71832-190">Další informace o šablonách aplikací v života naleznete v tématu [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span><span class="sxs-lookup"><span data-stu-id="71832-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="71832-191">Šablona "/todoList" obsahuje dva výrazy smyčky.</span><span class="sxs-lookup"><span data-stu-id="71832-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="71832-192">Vnější smyčka je `{{#each controller}}`a uvnitř smyčky je `{{#each todos}}`.</span><span class="sxs-lookup"><span data-stu-id="71832-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="71832-193">Následující kód ukazuje integrované zobrazení `Ember.Checkbox`, přizpůsobený `App.TodoItemEditView`a odkaz s akcí `deleteTodo`.</span><span class="sxs-lookup"><span data-stu-id="71832-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="71832-194">Třída `HtmlHelperExtensions` definovaná v Controllers/HtmlHelperExtensions. cs definuje pomocnou funkci pro ukládání souborů šablony do mezipaměti a vložení šablon, když je **ladění** v souboru Web. config nastaveno na **hodnotu true** .</span><span class="sxs-lookup"><span data-stu-id="71832-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExtensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="71832-195">Tato funkce se volá ze souboru zobrazení ASP.NET MVC definovaného v zobrazeních/domů/App. cshtml:</span><span class="sxs-lookup"><span data-stu-id="71832-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="71832-196">Volána bez argumentů, funkce vykreslí všechny soubory šablon ve složce Templates.</span><span class="sxs-lookup"><span data-stu-id="71832-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="71832-197">Můžete také zadat podsložku nebo konkrétní soubor šablony.</span><span class="sxs-lookup"><span data-stu-id="71832-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="71832-198">Je-li v souboru Web. config **hodnota** **Debug** , aplikace obsahuje položku sady prostředků "~/Bundles/templates".</span><span class="sxs-lookup"><span data-stu-id="71832-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="71832-199">Tato položka sady je přidána v BundleConfig.cs pomocí knihovny kompilátoru handlebars:</span><span class="sxs-lookup"><span data-stu-id="71832-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
