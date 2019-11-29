---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: Podpora akcí OData ve webovém rozhraní API 2 ASP.NET | Microsoft Docs
author: MikeWasson
description: 'V OData představují akce způsob, jak přidat chování na straně serveru, které není snadno definované jako operace CRUD u entit. Některá použití pro akce zahrnují: implementovat...'
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600353"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="541cc-104">Podpora akcí OData ve webovém rozhraní API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="541cc-104">Supporting OData Actions in ASP.NET Web API 2</span></span>

<span data-ttu-id="541cc-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="541cc-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="541cc-106">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="541cc-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="541cc-107">V OData představují *Akce* způsob, jak přidat chování na straně serveru, které není snadno definované jako operace CRUD u entit.</span><span class="sxs-lookup"><span data-stu-id="541cc-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="541cc-108">Mezi tato použití pro akce patří:</span><span class="sxs-lookup"><span data-stu-id="541cc-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="541cc-109">Implementace složitých transakcí.</span><span class="sxs-lookup"><span data-stu-id="541cc-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="541cc-110">Manipulace s několika entitami najednou.</span><span class="sxs-lookup"><span data-stu-id="541cc-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="541cc-111">Povoluje se aktualizace pouze některých vlastností entity.</span><span class="sxs-lookup"><span data-stu-id="541cc-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="541cc-112">Odesílají se informace na server, který není definovaný v entitě.</span><span class="sxs-lookup"><span data-stu-id="541cc-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="541cc-113">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="541cc-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="541cc-114">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="541cc-114">Web API 2</span></span>
> - <span data-ttu-id="541cc-115">OData verze 3</span><span class="sxs-lookup"><span data-stu-id="541cc-115">OData Version 3</span></span>
> - <span data-ttu-id="541cc-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="541cc-116">Entity Framework 6</span></span>

## <a name="example-rating-a-product"></a><span data-ttu-id="541cc-117">Příklad: hodnocení produktu</span><span class="sxs-lookup"><span data-stu-id="541cc-117">Example: Rating a Product</span></span>

<span data-ttu-id="541cc-118">V tomto příkladu chceme dovolit uživatelům hodnotit množství produktů a pak vystavit Průměrné hodnocení pro každý produkt.</span><span class="sxs-lookup"><span data-stu-id="541cc-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="541cc-119">V databázi budeme uchovávat seznam hodnocení, označených pro produkty.</span><span class="sxs-lookup"><span data-stu-id="541cc-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="541cc-120">Tady je model, který můžeme použít k reprezentaci hodnocení v Entity Framework:</span><span class="sxs-lookup"><span data-stu-id="541cc-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="541cc-121">Ale nechcete, aby klienti mohli publikovat objekt `ProductRating` do kolekce hodnocení.</span><span class="sxs-lookup"><span data-stu-id="541cc-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="541cc-122">V intuitivním případě je hodnocení přidruženo k kolekci Products a klient by měl pouze vystavit hodnotu hodnocení.</span><span class="sxs-lookup"><span data-stu-id="541cc-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="541cc-123">Proto namísto použití běžných operací CRUD definujeme akci, kterou může klient vyvolat na produkt.</span><span class="sxs-lookup"><span data-stu-id="541cc-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="541cc-124">V terminologii OData je akce *svázána* s entitami produktů.</span><span class="sxs-lookup"><span data-stu-id="541cc-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="541cc-125">Akce mají v serveru vedlejší účinky.</span><span class="sxs-lookup"><span data-stu-id="541cc-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="541cc-126">Z tohoto důvodu jsou vyvolány pomocí požadavků HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="541cc-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="541cc-127">Akce mohou mít parametry a návratové typy, které jsou popsány v metadatech služby.</span><span class="sxs-lookup"><span data-stu-id="541cc-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="541cc-128">Klient odešle parametry v textu požadavku a server odešle vrácenou hodnotu v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="541cc-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="541cc-129">Aby mohl klient vyvolat akci "hodnotit produkt", odešle příspěvek na identifikátor URI podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="541cc-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="541cc-130">Data v žádosti POST jsou jednoduše hodnocením produktu:</span><span class="sxs-lookup"><span data-stu-id="541cc-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="541cc-131">Deklarovat akci v model EDM (Entity Data Model)</span><span class="sxs-lookup"><span data-stu-id="541cc-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="541cc-132">V konfiguraci webového rozhraní API přidejte akci do modelu Entity Data Model (EDM):</span><span class="sxs-lookup"><span data-stu-id="541cc-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="541cc-133">Tento kód definuje "RateProduct" jako akci, kterou lze provést u entit produktu.</span><span class="sxs-lookup"><span data-stu-id="541cc-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="541cc-134">Deklaruje také, že akce přijímá parametr **int** s názvem "hodnocení" a vrátí hodnotu typu **int** .</span><span class="sxs-lookup"><span data-stu-id="541cc-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="541cc-135">Přidat akci do kontroleru</span><span class="sxs-lookup"><span data-stu-id="541cc-135">Add the Action to the Controller</span></span>

<span data-ttu-id="541cc-136">Akce "RateProduct" je svázána s entitami produktů.</span><span class="sxs-lookup"><span data-stu-id="541cc-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="541cc-137">Chcete-li implementovat akci, přidejte do kontroleru produktů metodu s názvem `RateProduct`:</span><span class="sxs-lookup"><span data-stu-id="541cc-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="541cc-138">Všimněte si, že název metody se shoduje s názvem akce v EDM.</span><span class="sxs-lookup"><span data-stu-id="541cc-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="541cc-139">Metoda má dva parametry:</span><span class="sxs-lookup"><span data-stu-id="541cc-139">The method has two parameters:</span></span>

- <span data-ttu-id="541cc-140">*Key*(klíč): klíč pro produkt, který se má ohodnotit.</span><span class="sxs-lookup"><span data-stu-id="541cc-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="541cc-141">*parametry*: slovník hodnot parametrů akce.</span><span class="sxs-lookup"><span data-stu-id="541cc-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="541cc-142">Pokud používáte výchozí konvence směrování, parametr klíče musí být pojmenovaný "klíč".</span><span class="sxs-lookup"><span data-stu-id="541cc-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="541cc-143">Je také důležité zahrnout atribut **[FromOdataUri]** , jak je znázorněno v příkladu.</span><span class="sxs-lookup"><span data-stu-id="541cc-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="541cc-144">Tento atribut oznamuje webovému rozhraní API použití pravidel syntaxe OData při analýze klíče z identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="541cc-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="541cc-145">Parametry akce získáte pomocí slovníku *parametrů* :</span><span class="sxs-lookup"><span data-stu-id="541cc-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="541cc-146">Pokud klient odešle parametry akce ve správném formátu, hodnota **ModelState. IsValid** má hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="541cc-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="541cc-147">V takovém případě můžete použít slovník **ODataActionParameters** k získání hodnot parametrů.</span><span class="sxs-lookup"><span data-stu-id="541cc-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="541cc-148">V tomto příkladu akce `RateProduct` přijímá jeden parametr s názvem "hodnocení".</span><span class="sxs-lookup"><span data-stu-id="541cc-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="541cc-149">Metadata akce</span><span class="sxs-lookup"><span data-stu-id="541cc-149">Action Metadata</span></span>

<span data-ttu-id="541cc-150">Pokud chcete zobrazit metadata služby, odešlete požadavek GET na/OData/$metadata.</span><span class="sxs-lookup"><span data-stu-id="541cc-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="541cc-151">Tady je část metadat, která deklaruje `RateProduct` akci:</span><span class="sxs-lookup"><span data-stu-id="541cc-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="541cc-152">Element **FunctionImport** deklaruje akci.</span><span class="sxs-lookup"><span data-stu-id="541cc-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="541cc-153">Většina polí je zřejmá, ale dvě se zaznamená:</span><span class="sxs-lookup"><span data-stu-id="541cc-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="541cc-154">S možností **vazby** znamená, že akci lze vyvolat v cílové entitě alespoň v některých časových okamžikech.</span><span class="sxs-lookup"><span data-stu-id="541cc-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="541cc-155">**IsAlwaysBindable** znamená, že akce může být vždy vyvolána v cílové entitě.</span><span class="sxs-lookup"><span data-stu-id="541cc-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="541cc-156">Rozdílem je, že některé akce jsou vždy k dispozici klientům, ale jiné akce mohou záviset na stavu entity.</span><span class="sxs-lookup"><span data-stu-id="541cc-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="541cc-157">Předpokládejme například, že definujete akci "koupit".</span><span class="sxs-lookup"><span data-stu-id="541cc-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="541cc-158">Můžete koupit jenom položku, která je na skladě.</span><span class="sxs-lookup"><span data-stu-id="541cc-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="541cc-159">Pokud je položka neskladovaná, klient nemůže tuto akci vyvolat.</span><span class="sxs-lookup"><span data-stu-id="541cc-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="541cc-160">Při definování EDM metoda **Akce** vytvoří akci Always-BIND:</span><span class="sxs-lookup"><span data-stu-id="541cc-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="541cc-161">Dále v tomto tématu se dozvíte o akcích, které nejsou vždy vázané na vazby (označované také jako *přechodné* akce).</span><span class="sxs-lookup"><span data-stu-id="541cc-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="541cc-162">Vyvolání akce</span><span class="sxs-lookup"><span data-stu-id="541cc-162">Invoking the Action</span></span>

<span data-ttu-id="541cc-163">Teď se podívejme, jak by klient tuto akci vyvolal.</span><span class="sxs-lookup"><span data-stu-id="541cc-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="541cc-164">Předpokládejme, že klient chce dát hodnocení 2 k produktu s ID = 4.</span><span class="sxs-lookup"><span data-stu-id="541cc-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="541cc-165">Tady je příklad zprávy s požadavkem s použitím formátu JSON pro tělo žádosti:</span><span class="sxs-lookup"><span data-stu-id="541cc-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="541cc-166">Tady je zpráva odpovědi:</span><span class="sxs-lookup"><span data-stu-id="541cc-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="541cc-167">Navázání akce na sadu entit</span><span class="sxs-lookup"><span data-stu-id="541cc-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="541cc-168">V předchozím příkladu je akce svázána s jedinou entitou: klient vyhodnotí jeden produkt.</span><span class="sxs-lookup"><span data-stu-id="541cc-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="541cc-169">Akci můžete také navazovat na kolekci entit.</span><span class="sxs-lookup"><span data-stu-id="541cc-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="541cc-170">Pouze proveďte následující změny:</span><span class="sxs-lookup"><span data-stu-id="541cc-170">Just make the following changes:</span></span>

<span data-ttu-id="541cc-171">V datovém modelu EDM přidejte akci do vlastnosti **kolekce** entity.</span><span class="sxs-lookup"><span data-stu-id="541cc-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="541cc-172">V metodě Controller vynechejte parametr *klíče* .</span><span class="sxs-lookup"><span data-stu-id="541cc-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="541cc-173">Klient nyní vyvolá akci pro sadu entit Products:</span><span class="sxs-lookup"><span data-stu-id="541cc-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="541cc-174">Akce s parametry kolekce</span><span class="sxs-lookup"><span data-stu-id="541cc-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="541cc-175">Akce mohou mít parametry, které přijímají kolekci hodnot.</span><span class="sxs-lookup"><span data-stu-id="541cc-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="541cc-176">V datovém modelu EDM použijte **&gt;CollectionParameter&lt;t** k deklaraci parametru.</span><span class="sxs-lookup"><span data-stu-id="541cc-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="541cc-177">Tato deklarace deklaruje parametr s názvem "hodnocení", který přebírá kolekci hodnot **int** .</span><span class="sxs-lookup"><span data-stu-id="541cc-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="541cc-178">V metodě Controller stále získáte hodnotu parametru z objektu **ODataActionParameters** , ale nyní je hodnotou hodnota typu **ICollection&lt;int&gt;** :</span><span class="sxs-lookup"><span data-stu-id="541cc-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="541cc-179">Přechodné akce</span><span class="sxs-lookup"><span data-stu-id="541cc-179">Transient Actions</span></span>

<span data-ttu-id="541cc-180">V příkladu "RateProduct" můžou uživatelé vždycky Ohodnotit produkt, takže tato akce je vždycky dostupná.</span><span class="sxs-lookup"><span data-stu-id="541cc-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="541cc-181">Některé akce ale závisí na stavu entity.</span><span class="sxs-lookup"><span data-stu-id="541cc-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="541cc-182">Například u služby pronájmu videa není akce "rezervace" vždy k dispozici.</span><span class="sxs-lookup"><span data-stu-id="541cc-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="541cc-183">(Záleží na tom, jestli je kopie tohoto videa dostupná.) Tento typ akce se nazývá *přechodná* akce.</span><span class="sxs-lookup"><span data-stu-id="541cc-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="541cc-184">V metadatech služby je přechodná akce **IsAlwaysBindable** rovna hodnotě false.</span><span class="sxs-lookup"><span data-stu-id="541cc-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="541cc-185">To je vlastně výchozí hodnota, takže metadata budou vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="541cc-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="541cc-186">Z tohoto důvodu: Pokud je akce přechodná, server musí klientovi sdělit, že je akce k dispozici.</span><span class="sxs-lookup"><span data-stu-id="541cc-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="541cc-187">Zahrnuje odkaz na akci v entitě.</span><span class="sxs-lookup"><span data-stu-id="541cc-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="541cc-188">Tady je příklad pro entitu video:</span><span class="sxs-lookup"><span data-stu-id="541cc-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="541cc-189">Vlastnost "#CheckOut" obsahuje odkaz na akci rezervace.</span><span class="sxs-lookup"><span data-stu-id="541cc-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="541cc-190">Pokud akce není k dispozici, server odkaz vynechá.</span><span class="sxs-lookup"><span data-stu-id="541cc-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="541cc-191">Chcete-li deklarovat přechodnou akci v modelu EDM, zavolejte metodu **TransientAction** :</span><span class="sxs-lookup"><span data-stu-id="541cc-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="541cc-192">Také je nutné zadat funkci, která vrátí odkaz akce pro danou entitu.</span><span class="sxs-lookup"><span data-stu-id="541cc-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="541cc-193">Tuto funkci nastavíte voláním **HasActionLink**.</span><span class="sxs-lookup"><span data-stu-id="541cc-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="541cc-194">Funkci můžete napsat jako výraz lambda:</span><span class="sxs-lookup"><span data-stu-id="541cc-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="541cc-195">Pokud je akce k dispozici, výraz lambda vrátí odkaz na akci.</span><span class="sxs-lookup"><span data-stu-id="541cc-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="541cc-196">Serializátor OData obsahuje tento odkaz při serializaci entity.</span><span class="sxs-lookup"><span data-stu-id="541cc-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="541cc-197">Pokud akce není k dispozici, funkce vrátí `null`.</span><span class="sxs-lookup"><span data-stu-id="541cc-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="541cc-198">Další materiály a zdroje informací</span><span class="sxs-lookup"><span data-stu-id="541cc-198">Additional Resources</span></span>

[<span data-ttu-id="541cc-199">Ukázka akcí OData</span><span class="sxs-lookup"><span data-stu-id="541cc-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
