---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 'Část 6: vytváření řadičů produktu a objednávek | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78524988"
---
# <a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="5d608-102">Část 6: vytváření řadičů produktu a objednávek</span><span class="sxs-lookup"><span data-stu-id="5d608-102">Part 6: Creating Product and Order Controllers</span></span>

<span data-ttu-id="5d608-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5d608-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5d608-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="5d608-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="5d608-105">Přidat kontroler produktů</span><span class="sxs-lookup"><span data-stu-id="5d608-105">Add a Products Controller</span></span>

<span data-ttu-id="5d608-106">Kontroler správců je pro uživatele, kteří mají oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="5d608-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="5d608-107">Zákazníci můžou na druhé straně zobrazovat produkty, ale nemůžou je vytvořit, aktualizovat ani odstranit.</span><span class="sxs-lookup"><span data-stu-id="5d608-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="5d608-108">Přístup k metodám post, PUT a DELETE můžeme snadno omezit, zatímco metody Get jsou otevřené.</span><span class="sxs-lookup"><span data-stu-id="5d608-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="5d608-109">Podívejte se ale na data vrácená produktem:</span><span class="sxs-lookup"><span data-stu-id="5d608-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="5d608-110">Vlastnost `ActualCost` by se neměla zobrazovat zákazníkům.</span><span class="sxs-lookup"><span data-stu-id="5d608-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="5d608-111">Řešením je definování *objektu pro přenos dat* (DTO), který obsahuje podmnožinu vlastností, které by měly být viditelné pro zákazníky.</span><span class="sxs-lookup"><span data-stu-id="5d608-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="5d608-112">Pro `ProductDTO` instancí budeme používat technologii LINQ to Project `Product` Instances.</span><span class="sxs-lookup"><span data-stu-id="5d608-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="5d608-113">Do složky modely přidejte třídu s názvem `ProductDTO`.</span><span class="sxs-lookup"><span data-stu-id="5d608-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="5d608-114">Nyní přidejte kontroler.</span><span class="sxs-lookup"><span data-stu-id="5d608-114">Now add the controller.</span></span> <span data-ttu-id="5d608-115">V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers.</span><span class="sxs-lookup"><span data-stu-id="5d608-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="5d608-116">Vyberte **Přidat**a pak vybrat **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="5d608-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="5d608-117">V dialogovém okně **Přidat řadič** pojmenujte kontrolér &quot;ProductsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="5d608-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="5d608-118">V části **Šablona**vyberte **prázdný kontroler rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="5d608-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="5d608-119">Nahraďte vše ve zdrojovém souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="5d608-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="5d608-120">Kontroler stále používá `OrdersContext` k dotazování databáze.</span><span class="sxs-lookup"><span data-stu-id="5d608-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="5d608-121">Místo toho, aby se přímo vracely `Product` Instances, voláme `MapProducts`, aby je provedla na `ProductDTO` instancí:</span><span class="sxs-lookup"><span data-stu-id="5d608-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="5d608-122">Metoda `MapProducts` vrací rozhraní **IQueryable**, takže můžeme výsledek sestavit s ostatními parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="5d608-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="5d608-123">Můžete to vidět v metodě `GetProduct`, která do dotazu přidá klauzuli **WHERE** :</span><span class="sxs-lookup"><span data-stu-id="5d608-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="5d608-124">Přidat řadič objednávek</span><span class="sxs-lookup"><span data-stu-id="5d608-124">Add an Orders Controller</span></span>

<span data-ttu-id="5d608-125">Dále přidejte kontroler, který umožňuje uživatelům vytvářet a zobrazovat objednávky.</span><span class="sxs-lookup"><span data-stu-id="5d608-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="5d608-126">Začneme s jiným DTO.</span><span class="sxs-lookup"><span data-stu-id="5d608-126">We'll start with another DTO.</span></span> <span data-ttu-id="5d608-127">V Průzkumník řešení klikněte pravým tlačítkem na složku modely a přidejte třídu s názvem `OrderDTO` použijte následující implementaci:</span><span class="sxs-lookup"><span data-stu-id="5d608-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="5d608-128">Nyní přidejte kontroler.</span><span class="sxs-lookup"><span data-stu-id="5d608-128">Now add the controller.</span></span> <span data-ttu-id="5d608-129">V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers.</span><span class="sxs-lookup"><span data-stu-id="5d608-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="5d608-130">Vyberte **Přidat**a pak vybrat **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="5d608-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="5d608-131">V dialogovém okně **Přidat řadič** nastavte následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="5d608-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="5d608-132">V části **název kontroleru**zadejte "OrdersController".</span><span class="sxs-lookup"><span data-stu-id="5d608-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="5d608-133">V části **Šablona**vyberte možnost kontroler API s akcemi čtení/zápisu pomocí Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="5d608-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="5d608-134">V části **třída modelu**vyberte &quot;Order (ProductStore. Models)&quot;.</span><span class="sxs-lookup"><span data-stu-id="5d608-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="5d608-135">V části **Třída kontextu dat**vyberte &quot;OrdersContext (ProductStore. Models)&quot;.</span><span class="sxs-lookup"><span data-stu-id="5d608-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="5d608-136">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="5d608-136">Click **Add**.</span></span> <span data-ttu-id="5d608-137">Tím se přidá soubor s názvem OrdersController.cs.</span><span class="sxs-lookup"><span data-stu-id="5d608-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="5d608-138">Dál je potřeba upravit výchozí implementaci kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5d608-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="5d608-139">Nejprve odstraňte metody `PutOrder` a `DeleteOrder`.</span><span class="sxs-lookup"><span data-stu-id="5d608-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="5d608-140">V této ukázce zákazníci nemůžou upravovat ani odstraňovat existující objednávky.</span><span class="sxs-lookup"><span data-stu-id="5d608-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="5d608-141">V reálné aplikaci budete potřebovat spoustu back-endové logiky, která tyto případy zpracovává.</span><span class="sxs-lookup"><span data-stu-id="5d608-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="5d608-142">(Například bylo objednávka již expedována?)</span><span class="sxs-lookup"><span data-stu-id="5d608-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="5d608-143">Změňte metodu `GetOrders` tak, aby vracela pouze objednávky, které patří uživateli:</span><span class="sxs-lookup"><span data-stu-id="5d608-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="5d608-144">Změňte metodu `GetOrder` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="5d608-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="5d608-145">Zde jsou změny, které jsme provedli v metodě:</span><span class="sxs-lookup"><span data-stu-id="5d608-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="5d608-146">Návratová hodnota je instance `OrderDTO` namísto `Order`.</span><span class="sxs-lookup"><span data-stu-id="5d608-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="5d608-147">Při dotazování databáze pro objednávku používáme metodu [DbQuery. include](https://msdn.microsoft.com/library/gg696395) k načtení souvisejících entit `OrderDetail` a `Product`.</span><span class="sxs-lookup"><span data-stu-id="5d608-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="5d608-148">Výsledek se sloučí s využitím projekce.</span><span class="sxs-lookup"><span data-stu-id="5d608-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="5d608-149">Odpověď HTTP bude obsahovat pole produktů s množstvím:</span><span class="sxs-lookup"><span data-stu-id="5d608-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="5d608-150">Tento formát je snazší, aby klienti využili oproti původnímu grafu objektů, který obsahuje vnořené entity (pořadí, podrobnosti a produkty).</span><span class="sxs-lookup"><span data-stu-id="5d608-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="5d608-151">Poslední metoda, kterou je třeba zvážit `PostOrder`.</span><span class="sxs-lookup"><span data-stu-id="5d608-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="5d608-152">V tuto chvíli Tato metoda používá instanci `Order`.</span><span class="sxs-lookup"><span data-stu-id="5d608-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="5d608-153">Ale zvažte, co se stane, když klient pošle text požadavku takto:</span><span class="sxs-lookup"><span data-stu-id="5d608-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="5d608-154">Toto je dobře strukturované pořadí a Entity Framework je Happily vložit do databáze.</span><span class="sxs-lookup"><span data-stu-id="5d608-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="5d608-155">Obsahuje však produktovou entitu, která nebyla dříve k dispozici.</span><span class="sxs-lookup"><span data-stu-id="5d608-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="5d608-156">Klient právě vytvořil v naší databázi nový produkt!</span><span class="sxs-lookup"><span data-stu-id="5d608-156">The client just created a new product in our database!</span></span> <span data-ttu-id="5d608-157">V případě, že se jim zobrazí objednávka Koala, bude to u oddělení pro plnění objednávek neočekávaně.</span><span class="sxs-lookup"><span data-stu-id="5d608-157">This will be a surprise to the order fulfillment department, when they see an order for koala bears.</span></span> <span data-ttu-id="5d608-158">Morální je, buďte pozorně opatrní na data, která přijmete v žádosti POST nebo PUT.</span><span class="sxs-lookup"><span data-stu-id="5d608-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="5d608-159">Chcete-li se tomuto problému vyhnout, změňte metodu `PostOrder` tak, aby převzala instanci `OrderDTO`.</span><span class="sxs-lookup"><span data-stu-id="5d608-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="5d608-160">`Order`vytvořte pomocí `OrderDTO`.</span><span class="sxs-lookup"><span data-stu-id="5d608-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="5d608-161">Všimněte si, že používáme vlastnosti `ProductID` a `Quantity` a ignorujeme všechny hodnoty, které klient poslal pro název produktu nebo cenu.</span><span class="sxs-lookup"><span data-stu-id="5d608-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="5d608-162">Pokud ID produktu není platné, porušuje se omezení cizího klíče v databázi a vložení se nezdaří, jak by mělo.</span><span class="sxs-lookup"><span data-stu-id="5d608-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="5d608-163">Toto je kompletní `PostOrder` metoda:</span><span class="sxs-lookup"><span data-stu-id="5d608-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="5d608-164">Nakonec přidejte do kontroleru atribut **autorizace** :</span><span class="sxs-lookup"><span data-stu-id="5d608-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="5d608-165">V současné době můžou objednávky vytvářet nebo zobrazovat jenom registrovaní uživatelé.</span><span class="sxs-lookup"><span data-stu-id="5d608-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5d608-166">[Předchozí](using-web-api-with-entity-framework-part-5.md)
> [Další](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="5d608-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
