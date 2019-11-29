---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: Podpora vztahů mezi entitami v OData V3 s webovým rozhraním API 2 | Microsoft Docs
author: MikeWasson
description: 'Většina datových sad definuje vztahy mezi entitami: zákazníci mají objednávky. knihy mají autory. produkty mají dodavatele. Pomocí OData můžou klienti přejít přes...'
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600316"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="0a3f4-104">Podpora vztahů mezi entitami v OData V3 pomocí webového rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="0a3f4-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>

<span data-ttu-id="0a3f4-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0a3f4-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="0a3f4-106">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="0a3f4-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="0a3f4-107">Většina datových sad definuje vztahy mezi entitami: zákazníci mají objednávky. knihy mají autory. produkty mají dodavatele.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="0a3f4-108">Pomocí OData můžou klienti přejít na vztahy mezi entitami.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="0a3f4-109">Pro daný produkt můžete najít dodavatele.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="0a3f4-110">Můžete také vytvořit nebo odebrat relace.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-110">You can also create or remove relationships.</span></span> <span data-ttu-id="0a3f4-111">Můžete například nastavit dodavatele produktu.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="0a3f4-112">V tomto kurzu se dozvíte, jak tyto operace podporovat v ASP.NET webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="0a3f4-113">Kurz sestaví na kurzu [Vytvoření koncového bodu OData V3 pomocí webového rozhraní API 2](creating-an-odata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="0a3f4-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0a3f4-114">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="0a3f4-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="0a3f4-115">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="0a3f4-115">Web API 2</span></span>
> - <span data-ttu-id="0a3f4-116">OData verze 3</span><span class="sxs-lookup"><span data-stu-id="0a3f4-116">OData Version 3</span></span>
> - <span data-ttu-id="0a3f4-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="0a3f4-117">Entity Framework 6</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="0a3f4-118">Přidat entitu dodavatele</span><span class="sxs-lookup"><span data-stu-id="0a3f4-118">Add a Supplier Entity</span></span>

<span data-ttu-id="0a3f4-119">Nejdřív musíme do našeho informačního kanálu OData přidat nový typ entity.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="0a3f4-120">Přidáme třídu `Supplier`.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="0a3f4-121">Tato třída používá řetězec pro klíč entity.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="0a3f4-122">V praxi může být méně častější než použití celočíselného klíče.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="0a3f4-123">Je ale vhodné vidět, jak OData zpracovává jiné typy klíčů Kromě celých čísel.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="0a3f4-124">V dalším kroku vytvoříme relaci přidáním vlastnosti `Supplier` do `Product` třídy:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="0a3f4-125">Přidejte novou **negenerickými** do třídy `ProductServiceContext`, aby Entity Framework v databázi zahrnovala tabulku `Supplier`.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="0a3f4-126">Do WebApiConfig.cs přidejte do modelu EDM entitu "dodavatelé":</span><span class="sxs-lookup"><span data-stu-id="0a3f4-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="0a3f4-127">Navigační vlastnosti</span><span class="sxs-lookup"><span data-stu-id="0a3f4-127">Navigation Properties</span></span>

<span data-ttu-id="0a3f4-128">Pokud chcete získat dodavatele pro určitý produkt, klient odešle požadavek GET:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="0a3f4-129">Zde je pro typ `Product` navigační vlastnost "dodavatel".</span><span class="sxs-lookup"><span data-stu-id="0a3f4-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="0a3f4-130">V tomto případě `Supplier` odkazuje na jednu položku, ale navigační vlastnost může také vracet kolekci (vztah 1: n nebo m:n).</span><span class="sxs-lookup"><span data-stu-id="0a3f4-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="0a3f4-131">Pro podporu tohoto požadavku přidejte následující metodu do třídy `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="0a3f4-132">Parametr *Key* je klíč produktu.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="0a3f4-133">Metoda vrátí související entitu&#8212;v tomto případě instance `Supplier`.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-133">The method returns the related entity&#8212;in this case, a `Supplier` instance.</span></span> <span data-ttu-id="0a3f4-134">Název metody a název parametru jsou důležité.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="0a3f4-135">Obecně platí, že pokud je navigační vlastnost pojmenována "X", je nutné přidat metodu s názvem "GetX".</span><span class="sxs-lookup"><span data-stu-id="0a3f4-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="0a3f4-136">Metoda musí přijmout parametr s názvem "*Key*", který odpovídá datovému typu nadřazeného klíče.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="0a3f4-137">Je také důležité zahrnout do parametru *Key* atribut **[FromOdataUri]** .</span><span class="sxs-lookup"><span data-stu-id="0a3f4-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="0a3f4-138">Tento atribut oznamuje webovému rozhraní API použití pravidel syntaxe OData při analýze klíče z identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="0a3f4-139">Vytváření a odstraňování odkazů</span><span class="sxs-lookup"><span data-stu-id="0a3f4-139">Creating and Deleting Links</span></span>

<span data-ttu-id="0a3f4-140">OData podporuje vytváření nebo odebírání vztahů mezi dvěma entitami.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="0a3f4-141">V terminologii OData je vztah "odkaz".</span><span class="sxs-lookup"><span data-stu-id="0a3f4-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="0a3f4-142">Každý odkaz má identifikátor URI s formulářem *entity*/$Links/*entity*.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="0a3f4-143">Například odkaz z produktu na dodavatel vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="0a3f4-144">Chcete-li vytvořit nový odkaz, klient odešle požadavek POST do identifikátoru URI odkazu.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="0a3f4-145">Tělo požadavku je identifikátor URI cílové entity.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="0a3f4-146">Předpokládejme například, že je k dispozici dodavatel s klíčem "CTSO".</span><span class="sxs-lookup"><span data-stu-id="0a3f4-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="0a3f4-147">Pokud chcete vytvořit odkaz z "Product (1)" na "dodavatel (' CTSO ')", klient odešle požadavek podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="0a3f4-148">Chcete-li odstranit odkaz, klient pošle požadavek na odstranění identifikátoru URI odkazu.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="0a3f4-149">**Vytváření odkazů**</span><span class="sxs-lookup"><span data-stu-id="0a3f4-149">**Creating Links**</span></span>

<span data-ttu-id="0a3f4-150">Chcete-li povolit klientovi vytváření odkazů na dodavatele produktů, přidejte následující kód do třídy `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="0a3f4-151">Tato metoda přijímá tři parametry:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-151">This method takes three parameters:</span></span>

- <span data-ttu-id="0a3f4-152">*klíč*: klíč k nadřazené entitě (produkt)</span><span class="sxs-lookup"><span data-stu-id="0a3f4-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="0a3f4-153">*navigationProperty*: název vlastnosti navigace.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="0a3f4-154">V tomto příkladu je jedinou platnou navigační vlastností "dodavatel".</span><span class="sxs-lookup"><span data-stu-id="0a3f4-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="0a3f4-155">*odkaz*: identifikátor URI OData související entity.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="0a3f4-156">Tato hodnota je pořízena z textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-156">This value is taken from the request body.</span></span> <span data-ttu-id="0a3f4-157">Identifikátor URI odkazu může být například "`http://localhost/odata/Suppliers('CTSO')`, což znamená dodavatel s ID =" CTSO ".</span><span class="sxs-lookup"><span data-stu-id="0a3f4-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="0a3f4-158">Metoda používá odkaz k vyhledání dodavatele.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="0a3f4-159">Pokud je nalezen shodný dodavatel, metoda nastaví vlastnost `Product.Supplier` a uloží výsledek do databáze.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="0a3f4-160">Závažná součást analyzuje identifikátor URI odkazu.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="0a3f4-161">V podstatě potřebujete simulovat výsledek odeslání žádosti o získání na tento identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="0a3f4-162">Následující pomocná metoda ukazuje, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="0a3f4-163">Metoda vyvolá proces směrování webového rozhraní API a vrátí zpět instanci **ODataPath** , která představuje analyzovanou cestu OData.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="0a3f4-164">U identifikátoru URI odkazu by měl být jeden z segmentů klíč entity.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="0a3f4-165">(Pokud ne, klient odeslal chybný identifikátor URI.)</span><span class="sxs-lookup"><span data-stu-id="0a3f4-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="0a3f4-166">**Odstraňování odkazů**</span><span class="sxs-lookup"><span data-stu-id="0a3f4-166">**Deleting Links**</span></span>

<span data-ttu-id="0a3f4-167">Chcete-li odstranit odkaz, přidejte následující kód do třídy `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="0a3f4-168">V tomto příkladu je navigační vlastnost jedinou entitou `Supplier`.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="0a3f4-169">Pokud je navigační vlastnost kolekce, identifikátor URI pro odstranění odkazu musí obsahovat klíč pro související entitu.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="0a3f4-170">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="0a3f4-171">Tato žádost odebere objednávku 1 od zákazníka 1.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="0a3f4-172">V takovém případě bude mít metoda DeleteLink fungují následující signaturu:</span><span class="sxs-lookup"><span data-stu-id="0a3f4-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="0a3f4-173">Parametr *relatedKey* poskytuje klíč pro související entitu.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="0a3f4-174">Takže v metodě `DeleteLink` vyhledejte primární entitu pomocí parametru *Key* , vyhledejte související entitu pomocí parametru *relatedKey* a pak odeberte přidružení.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="0a3f4-175">V závislosti na datovém modelu možná budete muset implementovat obě verze `DeleteLink`.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="0a3f4-176">Webové rozhraní API bude volat správnou verzi na základě identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="0a3f4-176">Web API will call the correct version based on the request URI.</span></span>
