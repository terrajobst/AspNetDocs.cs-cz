---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 'Část 3: vytvoření kontroleru správce | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600033"
---
# <a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="66ac7-102">3\. část: vytvoření kontroleru správce</span><span class="sxs-lookup"><span data-stu-id="66ac7-102">Part 3: Creating an Admin Controller</span></span>

<span data-ttu-id="66ac7-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="66ac7-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="66ac7-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="66ac7-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="66ac7-105">Přidat kontroler správce</span><span class="sxs-lookup"><span data-stu-id="66ac7-105">Add an Admin Controller</span></span>

<span data-ttu-id="66ac7-106">V této části přidáme kontroler webového rozhraní API, který podporuje operace CRUD (vytváření, čtení, aktualizace a odstraňování) na produktech.</span><span class="sxs-lookup"><span data-stu-id="66ac7-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="66ac7-107">Kontroler použije Entity Framework ke komunikaci s databázovou vrstvou.</span><span class="sxs-lookup"><span data-stu-id="66ac7-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="66ac7-108">Pouze správci budou moci použít tento kontroler.</span><span class="sxs-lookup"><span data-stu-id="66ac7-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="66ac7-109">Zákazníci budou k produktům přistupovat přes jiný kontroler.</span><span class="sxs-lookup"><span data-stu-id="66ac7-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="66ac7-110">V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers.</span><span class="sxs-lookup"><span data-stu-id="66ac7-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="66ac7-111">Vyberte **Přidat** a potom **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="66ac7-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="66ac7-112">V dialogovém okně **Přidat řadič zadejte** název kontroleru `AdminController`.</span><span class="sxs-lookup"><span data-stu-id="66ac7-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="66ac7-113">V části **Šablona**vyberte &quot;Controller rozhraní API s akcemi čtení/zápisu pomocí Entity Framework&quot;.</span><span class="sxs-lookup"><span data-stu-id="66ac7-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="66ac7-114">V části **třída modelu**vyberte produkt (ProductStore. Models).</span><span class="sxs-lookup"><span data-stu-id="66ac7-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="66ac7-115">V části **datový kontext**vyberte&lt;nový kontext dat&gt;.</span><span class="sxs-lookup"><span data-stu-id="66ac7-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="66ac7-116">Pokud rozevírací seznam **třídy modelu** nezobrazuje žádné třídy modelu, ujistěte se, že jste projekt kompilováni.</span><span class="sxs-lookup"><span data-stu-id="66ac7-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="66ac7-117">Entity Framework používá reflexi, takže potřebuje zkompilované sestavení.</span><span class="sxs-lookup"><span data-stu-id="66ac7-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>

<span data-ttu-id="66ac7-118">Vybráním možnosti&lt;nový kontext dat&gt;se otevře dialogové okno **nový kontext** dat.</span><span class="sxs-lookup"><span data-stu-id="66ac7-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="66ac7-119">Pojmenujte `ProductStore.Models.OrdersContext`datový kontext.</span><span class="sxs-lookup"><span data-stu-id="66ac7-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="66ac7-120">Kliknutím na tlačítko **OK** zavřete dialogové okno **nový kontext dat** .</span><span class="sxs-lookup"><span data-stu-id="66ac7-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="66ac7-121">V dialogovém okně **Přidat řadič** klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="66ac7-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="66ac7-122">Tady je postup přidaný do projektu:</span><span class="sxs-lookup"><span data-stu-id="66ac7-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="66ac7-123">Třída s názvem `OrdersContext`, která je odvozena z **DbContext**.</span><span class="sxs-lookup"><span data-stu-id="66ac7-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="66ac7-124">Tato třída poskytuje připevňování mezi modely POCO a databází.</span><span class="sxs-lookup"><span data-stu-id="66ac7-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="66ac7-125">Kontroler webového rozhraní API s názvem `AdminController`.</span><span class="sxs-lookup"><span data-stu-id="66ac7-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="66ac7-126">Tento kontroler podporuje operace CRUD pro instance `Product`.</span><span class="sxs-lookup"><span data-stu-id="66ac7-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="66ac7-127">Používá třídu `OrdersContext` ke komunikaci s Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="66ac7-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="66ac7-128">Nový připojovací řetězec databáze v souboru Web. config.</span><span class="sxs-lookup"><span data-stu-id="66ac7-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="66ac7-129">Otevřete soubor OrdersContext.cs.</span><span class="sxs-lookup"><span data-stu-id="66ac7-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="66ac7-130">Všimněte si, že konstruktor určuje název připojovacího řetězce databáze.</span><span class="sxs-lookup"><span data-stu-id="66ac7-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="66ac7-131">Tento název odkazuje na připojovací řetězec, který byl přidán do souboru Web. config.</span><span class="sxs-lookup"><span data-stu-id="66ac7-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="66ac7-132">Do `OrdersContext` třídy přidejte následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="66ac7-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="66ac7-133">**Negenerickými** představuje sadu entit, na které se dá dotazovat.</span><span class="sxs-lookup"><span data-stu-id="66ac7-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="66ac7-134">Zde je kompletní seznam pro třídu `OrdersContext`:</span><span class="sxs-lookup"><span data-stu-id="66ac7-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="66ac7-135">Třída `AdminController` definuje pět metod, které implementují základní funkce CRUD.</span><span class="sxs-lookup"><span data-stu-id="66ac7-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="66ac7-136">Každá metoda odpovídá identifikátoru URI, který může klient vyvolat:</span><span class="sxs-lookup"><span data-stu-id="66ac7-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="66ac7-137">Metoda kontroleru</span><span class="sxs-lookup"><span data-stu-id="66ac7-137">Controller Method</span></span> | <span data-ttu-id="66ac7-138">Popis</span><span class="sxs-lookup"><span data-stu-id="66ac7-138">Description</span></span> | <span data-ttu-id="66ac7-139">URI</span><span class="sxs-lookup"><span data-stu-id="66ac7-139">URI</span></span> | <span data-ttu-id="66ac7-140">HTTP – metoda</span><span class="sxs-lookup"><span data-stu-id="66ac7-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="66ac7-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="66ac7-141">GetProducts</span></span> | <span data-ttu-id="66ac7-142">Načte všechny produkty.</span><span class="sxs-lookup"><span data-stu-id="66ac7-142">Gets all products.</span></span> | <span data-ttu-id="66ac7-143">rozhraní API/produkty</span><span class="sxs-lookup"><span data-stu-id="66ac7-143">api/products</span></span> | <span data-ttu-id="66ac7-144">GET</span><span class="sxs-lookup"><span data-stu-id="66ac7-144">GET</span></span> |
| <span data-ttu-id="66ac7-145">Getproduct</span><span class="sxs-lookup"><span data-stu-id="66ac7-145">GetProduct</span></span> | <span data-ttu-id="66ac7-146">Vyhledá produkt podle ID.</span><span class="sxs-lookup"><span data-stu-id="66ac7-146">Finds a product by ID.</span></span> | <span data-ttu-id="66ac7-147">API/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="66ac7-147">api/products/*id*</span></span> | <span data-ttu-id="66ac7-148">GET</span><span class="sxs-lookup"><span data-stu-id="66ac7-148">GET</span></span> |
| <span data-ttu-id="66ac7-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="66ac7-149">PutProduct</span></span> | <span data-ttu-id="66ac7-150">Aktualizuje produkt.</span><span class="sxs-lookup"><span data-stu-id="66ac7-150">Updates a product.</span></span> | <span data-ttu-id="66ac7-151">API/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="66ac7-151">api/products/*id*</span></span> | <span data-ttu-id="66ac7-152">PŘEVÉST</span><span class="sxs-lookup"><span data-stu-id="66ac7-152">PUT</span></span> |
| <span data-ttu-id="66ac7-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="66ac7-153">PostProduct</span></span> | <span data-ttu-id="66ac7-154">Vytvoří nový produkt.</span><span class="sxs-lookup"><span data-stu-id="66ac7-154">Creates a new product.</span></span> | <span data-ttu-id="66ac7-155">rozhraní API/produkty</span><span class="sxs-lookup"><span data-stu-id="66ac7-155">api/products</span></span> | <span data-ttu-id="66ac7-156">POST</span><span class="sxs-lookup"><span data-stu-id="66ac7-156">POST</span></span> |
| <span data-ttu-id="66ac7-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="66ac7-157">DeleteProduct</span></span> | <span data-ttu-id="66ac7-158">Odstraní produkt.</span><span class="sxs-lookup"><span data-stu-id="66ac7-158">Deletes a product.</span></span> | <span data-ttu-id="66ac7-159">API/Products/*ID*</span><span class="sxs-lookup"><span data-stu-id="66ac7-159">api/products/*id*</span></span> | <span data-ttu-id="66ac7-160">DELETE</span><span class="sxs-lookup"><span data-stu-id="66ac7-160">DELETE</span></span> |

<span data-ttu-id="66ac7-161">Každá metoda volá do `OrdersContext` dotazování databáze.</span><span class="sxs-lookup"><span data-stu-id="66ac7-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="66ac7-162">Metody, které mění kolekci (PUT, POST a DELETE) volání `db.SaveChanges`, aby zachovaly změny v databázi.</span><span class="sxs-lookup"><span data-stu-id="66ac7-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="66ac7-163">Řadiče se vytvoří na žádost HTTP a pak se vyřadí, takže je nutné zachovat změny před tím, než se metoda vrátí.</span><span class="sxs-lookup"><span data-stu-id="66ac7-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="66ac7-164">Přidat inicializátor databáze</span><span class="sxs-lookup"><span data-stu-id="66ac7-164">Add a Database Initializer</span></span>

<span data-ttu-id="66ac7-165">Entity Framework má skvělé funkce, která umožňuje naplnit databázi při spuštění a automaticky znovu vytvořit databázi vždy, když se změní modely.</span><span class="sxs-lookup"><span data-stu-id="66ac7-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="66ac7-166">Tato funkce je užitečná při vývoji, protože máte vždy nějaká testovací data, a to i v případě, že změníte modely.</span><span class="sxs-lookup"><span data-stu-id="66ac7-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="66ac7-167">V Průzkumník řešení klikněte pravým tlačítkem na složku modely a vytvořte novou třídu s názvem `OrdersContextInitializer`.</span><span class="sxs-lookup"><span data-stu-id="66ac7-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="66ac7-168">Vložit do následující implementace:</span><span class="sxs-lookup"><span data-stu-id="66ac7-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="66ac7-169">Díky dědění z třídy **DropCreateDatabaseIfModelChanges** oznamujeme Entity Framework k vyřazení databáze pokaždé, když upravíte třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="66ac7-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="66ac7-170">Když Entity Framework vytvoří (nebo znovu vytvoří) databázi, zavolá metodu **počáteční** hodnoty k naplnění tabulek.</span><span class="sxs-lookup"><span data-stu-id="66ac7-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="66ac7-171">Metoda **počáteční** hodnoty používáme k přidání některých ukázkových produktů plus Příklad objednávky.</span><span class="sxs-lookup"><span data-stu-id="66ac7-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="66ac7-172">Tato funkce je ideální pro testování, ale nepoužívejte třídu **DropCreateDatabaseIfModelChanges** v produkčním prostředí, protože byste mohli přijít o data, pokud někdo změní třídu modelu.</span><span class="sxs-lookup"><span data-stu-id="66ac7-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="66ac7-173">Dále otevřete Global. asax a přidejte následující kód do **aplikace\_spustit** metodu:</span><span class="sxs-lookup"><span data-stu-id="66ac7-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="66ac7-174">Odeslat žádost do kontroleru</span><span class="sxs-lookup"><span data-stu-id="66ac7-174">Send a Request to the Controller</span></span>

<span data-ttu-id="66ac7-175">V tuto chvíli jsme nenapsali žádný kód klienta, ale můžete vyvolat webové rozhraní API pomocí webového prohlížeče nebo ladicího nástroje HTTP, jako je [Fiddler](http://www.fiddler2.com/fiddler2/).</span><span class="sxs-lookup"><span data-stu-id="66ac7-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="66ac7-176">V aplikaci Visual Studio stiskněte klávesu F5 pro spuštění ladění.</span><span class="sxs-lookup"><span data-stu-id="66ac7-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="66ac7-177">Webový prohlížeč se otevře pro `http://localhost:*portnum*/`, kde *portnum* je nějaké číslo portu.</span><span class="sxs-lookup"><span data-stu-id="66ac7-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="66ac7-178">Odešle požadavek HTTP na`http://localhost:*portnum*/api/admin`.</span><span class="sxs-lookup"><span data-stu-id="66ac7-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="66ac7-179">První požadavek může být pomalý, protože Entity Framework musí vytvořit a naplnit databázi.</span><span class="sxs-lookup"><span data-stu-id="66ac7-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="66ac7-180">Odpověď by měla vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="66ac7-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="66ac7-181">[Předchozí](using-web-api-with-entity-framework-part-2.md)
> [Další](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="66ac7-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
