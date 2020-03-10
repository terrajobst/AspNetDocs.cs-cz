---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: Akce a funkce v OData v4 pomocí webového rozhraní API ASP.NET 2,2 | Microsoft Docs
author: MikeWasson
description: V rámci OData představují akce a funkce způsob, jak přidat chování na straně serveru, která nejsou snadno definovaná jako operace CRUD u entit. V tomto kurzu se dozvíte, jak...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556222"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="c086f-104">Akce a funkce v OData v4 pomocí webového rozhraní API ASP.NET 2,2</span><span class="sxs-lookup"><span data-stu-id="c086f-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="c086f-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c086f-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="c086f-106">V rámci OData představují akce a funkce způsob, jak přidat chování na straně serveru, která nejsou snadno definovaná jako operace CRUD u entit.</span><span class="sxs-lookup"><span data-stu-id="c086f-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="c086f-107">V tomto kurzu se dozvíte, jak přidat akce a funkce do koncového bodu OData v4 pomocí webového rozhraní API 2,2.</span><span class="sxs-lookup"><span data-stu-id="c086f-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="c086f-108">Kurz sestaví na kurzu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní API 2 ASP.NET](create-an-odata-v4-endpoint.md) .</span><span class="sxs-lookup"><span data-stu-id="c086f-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c086f-109">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="c086f-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="c086f-110">Webové rozhraní API 2,2</span><span class="sxs-lookup"><span data-stu-id="c086f-110">Web API 2.2</span></span>
> - <span data-ttu-id="c086f-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="c086f-111">OData v4</span></span>
> - <span data-ttu-id="c086f-112">Visual Studio 2013 (Stáhněte si Visual Studio 2017 [tady](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="c086f-112">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="c086f-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c086f-113">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="c086f-114">Verze kurzů</span><span class="sxs-lookup"><span data-stu-id="c086f-114">Tutorial versions</span></span>
>
> <span data-ttu-id="c086f-115">Pro OData verze 3 se podívejte [na téma akce OData ve webovém rozhraní API 2 pro ASP.NET](../odata-v3/odata-actions.md).</span><span class="sxs-lookup"><span data-stu-id="c086f-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="c086f-116">Rozdíl mezi *akcemi* a *funkcemi* je, že akce mohou mít vedlejší účinky a funkce ne.</span><span class="sxs-lookup"><span data-stu-id="c086f-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="c086f-117">Akce a funkce mohou vracet data.</span><span class="sxs-lookup"><span data-stu-id="c086f-117">Both actions and functions can return data.</span></span> <span data-ttu-id="c086f-118">Mezi tato použití pro akce patří:</span><span class="sxs-lookup"><span data-stu-id="c086f-118">Some uses for actions include:</span></span>

- <span data-ttu-id="c086f-119">Komplexní transakce.</span><span class="sxs-lookup"><span data-stu-id="c086f-119">Complex transactions.</span></span>
- <span data-ttu-id="c086f-120">Manipulace s několika entitami najednou.</span><span class="sxs-lookup"><span data-stu-id="c086f-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="c086f-121">Povoluje se aktualizace pouze některých vlastností entity.</span><span class="sxs-lookup"><span data-stu-id="c086f-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="c086f-122">Odesílají se data, která nejsou entitou.</span><span class="sxs-lookup"><span data-stu-id="c086f-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="c086f-123">Funkce jsou užitečné pro vracení informací, které neodpovídají přímo entitě nebo kolekci.</span><span class="sxs-lookup"><span data-stu-id="c086f-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="c086f-124">Akce (nebo funkce) může cílit na jednu entitu nebo kolekci.</span><span class="sxs-lookup"><span data-stu-id="c086f-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="c086f-125">V terminologii OData je to *vazba*.</span><span class="sxs-lookup"><span data-stu-id="c086f-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="c086f-126">Můžete mít také &quot;nevázané&quot; akce nebo funkce, které se nazývají jako statické operace ve službě.</span><span class="sxs-lookup"><span data-stu-id="c086f-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="c086f-127">Příklad: Přidání akce</span><span class="sxs-lookup"><span data-stu-id="c086f-127">Example: Adding an Action</span></span>

<span data-ttu-id="c086f-128">Pojďme definovat akci pro hodnocení produktu.</span><span class="sxs-lookup"><span data-stu-id="c086f-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="c086f-129">Tento kurz sestaví v kurzu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní API 2 ASP.NET](create-an-odata-v4-endpoint.md) .</span><span class="sxs-lookup"><span data-stu-id="c086f-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="c086f-130">Nejdřív přidejte `ProductRating` model, který bude reprezentovat hodnocení.</span><span class="sxs-lookup"><span data-stu-id="c086f-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="c086f-131">Přidejte také **negenerickými** do třídy `ProductsContext`, aby EF vytvořil v databázi tabulku hodnocení.</span><span class="sxs-lookup"><span data-stu-id="c086f-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="c086f-132">Přidat akci do modelu EDM</span><span class="sxs-lookup"><span data-stu-id="c086f-132">Add the Action to the EDM</span></span>

<span data-ttu-id="c086f-133">Do WebApiConfig.cs přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="c086f-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="c086f-134">Metoda **EntityTypeConfiguration. Action** přidá akci do modelu Entity Data Model (EDM).</span><span class="sxs-lookup"><span data-stu-id="c086f-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="c086f-135">Metoda **parametru** určuje typový parametr pro akci.</span><span class="sxs-lookup"><span data-stu-id="c086f-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="c086f-136">Tento kód také nastaví obor názvů pro EDM.</span><span class="sxs-lookup"><span data-stu-id="c086f-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="c086f-137">Obor názvů záleží na tom, že identifikátor URI pro akci obsahuje plně kvalifikovaný název akce:</span><span class="sxs-lookup"><span data-stu-id="c086f-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="c086f-138">V typické konfiguraci služby IIS bude tečka v této adrese URL způsobit, že služba IIS vrátí chybu 404.</span><span class="sxs-lookup"><span data-stu-id="c086f-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="c086f-139">Můžete to vyřešit přidáním následujícího oddílu do souboru Web. config:</span><span class="sxs-lookup"><span data-stu-id="c086f-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="c086f-140">Přidat metodu kontroleru pro akci</span><span class="sxs-lookup"><span data-stu-id="c086f-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="c086f-141">Pokud chcete povolit akci&quot; &quot;míry, přidejte do `ProductsController`následující metodu:</span><span class="sxs-lookup"><span data-stu-id="c086f-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="c086f-142">Všimněte si, že název metody se shoduje s názvem akce.</span><span class="sxs-lookup"><span data-stu-id="c086f-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="c086f-143">Atribut **[HTTPPOST]** určuje způsob, jakým je metoda HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="c086f-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="c086f-144">K vyvolání akce klient odešle požadavek HTTP POST podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="c086f-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="c086f-145">Akce &quot;míra&quot; je vázána na instance produktu, takže identifikátor URI pro akci je plně kvalifikovaný název akce připojený k identifikátoru URI entity.</span><span class="sxs-lookup"><span data-stu-id="c086f-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="c086f-146">(Odvoláme, že obor názvů EDM nastavíme na &quot;ProductService&quot;, takže plně kvalifikovaný název akce je &quot;ProductService. Rate&quot;.)</span><span class="sxs-lookup"><span data-stu-id="c086f-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="c086f-147">Tělo požadavku obsahuje parametry akce jako datovou část JSON.</span><span class="sxs-lookup"><span data-stu-id="c086f-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="c086f-148">Webové rozhraní API automaticky převede datovou část JSON na objekt **ODataActionParameters** , což je pouze slovník hodnot parametrů.</span><span class="sxs-lookup"><span data-stu-id="c086f-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="c086f-149">Tento slovník použijte pro přístup k parametrům v metodě kontroleru.</span><span class="sxs-lookup"><span data-stu-id="c086f-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="c086f-150">Pokud klient odešle parametry akce v nesprávném formátu, hodnota **ModelState. IsValid** je false.</span><span class="sxs-lookup"><span data-stu-id="c086f-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="c086f-151">Ověřte tento příznak v metodě kontroleru a vraťte chybu, pokud je vlastnost **IsValid** false.</span><span class="sxs-lookup"><span data-stu-id="c086f-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="c086f-152">Příklad: Přidání funkce</span><span class="sxs-lookup"><span data-stu-id="c086f-152">Example: Adding a Function</span></span>

<span data-ttu-id="c086f-153">Nyní přidáme funkci OData, která vrátí nejlevnější produkt.</span><span class="sxs-lookup"><span data-stu-id="c086f-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="c086f-154">Stejně jako dřív je prvním krokem přidání funkce do modelu EDM.</span><span class="sxs-lookup"><span data-stu-id="c086f-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="c086f-155">Do WebApiConfig.cs přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="c086f-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="c086f-156">V tomto případě je funkce vázána na kolekci Products, nikoli na jednotlivé instance produktu.</span><span class="sxs-lookup"><span data-stu-id="c086f-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="c086f-157">Klienti vyvolávají funkci odesláním žádosti o získání:</span><span class="sxs-lookup"><span data-stu-id="c086f-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="c086f-158">Toto je metoda kontroleru pro tuto funkci:</span><span class="sxs-lookup"><span data-stu-id="c086f-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="c086f-159">Všimněte si, že název metody se shoduje s názvem funkce.</span><span class="sxs-lookup"><span data-stu-id="c086f-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="c086f-160">Atribut **[HttpGet]** určuje metodu metodou GET protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="c086f-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="c086f-161">Toto je odpověď HTTP:</span><span class="sxs-lookup"><span data-stu-id="c086f-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="c086f-162">Příklad: Přidání nevázané funkce</span><span class="sxs-lookup"><span data-stu-id="c086f-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="c086f-163">Předchozí příklad byl funkce vázaný na kolekci.</span><span class="sxs-lookup"><span data-stu-id="c086f-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="c086f-164">V tomto dalším příkladu vytvoříme *nevázanou* funkci.</span><span class="sxs-lookup"><span data-stu-id="c086f-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="c086f-165">Nevázané funkce se volají jako statické operace ve službě.</span><span class="sxs-lookup"><span data-stu-id="c086f-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="c086f-166">Funkce v tomto příkladu vrátí daň z prodeje pro daný poštovní směrovací číslo.</span><span class="sxs-lookup"><span data-stu-id="c086f-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="c086f-167">Do souboru WebApiConfig Přidejte funkci do modelu EDM:</span><span class="sxs-lookup"><span data-stu-id="c086f-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="c086f-168">Všimněte si, že voláme **Functions** přímo na **ODataModelBuilder**místo typu entity nebo kolekce.</span><span class="sxs-lookup"><span data-stu-id="c086f-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="c086f-169">Tvůrce modelu tak informuje, že funkce není vázaná.</span><span class="sxs-lookup"><span data-stu-id="c086f-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="c086f-170">Zde je metoda kontroleru, která implementuje funkci:</span><span class="sxs-lookup"><span data-stu-id="c086f-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="c086f-171">Nezáleží na tom, který řídicí řadič webového rozhraní API tuto metodu umístí.</span><span class="sxs-lookup"><span data-stu-id="c086f-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="c086f-172">Můžete ji umístit do `ProductsController`nebo definovat samostatný kontroler.</span><span class="sxs-lookup"><span data-stu-id="c086f-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="c086f-173">Atribut **[ODataRoute]** definuje šablonu identifikátoru URI pro funkci.</span><span class="sxs-lookup"><span data-stu-id="c086f-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="c086f-174">Tady je příklad žádosti klienta:</span><span class="sxs-lookup"><span data-stu-id="c086f-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="c086f-175">Odpověď HTTP:</span><span class="sxs-lookup"><span data-stu-id="c086f-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
