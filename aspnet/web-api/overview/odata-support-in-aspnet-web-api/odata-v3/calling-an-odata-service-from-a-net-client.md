---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: Volání služby OData z klienta .NET (C#) | Microsoft Docs
author: MikeWasson
description: V tomto kurzu se dozvíte, jak volat službu OData C# z klientské aplikace. Verze softwaru používané v tomto kurzu Visual Studio 2013 (funguje s Visual S...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600395"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a><span data-ttu-id="921dd-104">Volání služby OData z klienta .NET (C#)</span><span class="sxs-lookup"><span data-stu-id="921dd-104">Calling an OData Service From a .NET Client (C#)</span></span>

<span data-ttu-id="921dd-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="921dd-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="921dd-106">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="921dd-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="921dd-107">V tomto kurzu se dozvíte, jak volat službu OData C# z klientské aplikace.</span><span class="sxs-lookup"><span data-stu-id="921dd-107">This tutorial shows how to call an OData service from a C# client application.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="921dd-108">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="921dd-108">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="921dd-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (funguje se sadou Visual Studio 2012)</span><span class="sxs-lookup"><span data-stu-id="921dd-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (works with Visual Studio 2012)</span></span>
> - [<span data-ttu-id="921dd-110">Klientská knihovna pro WCF Data Services</span><span class="sxs-lookup"><span data-stu-id="921dd-110">WCF Data Services Client Library</span></span>](https://msdn.microsoft.com/library/cc668772.aspx)
> - <span data-ttu-id="921dd-111">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="921dd-111">Web API 2.</span></span> <span data-ttu-id="921dd-112">(Ukázková Služba OData je sestavená pomocí webového rozhraní API 2, ale klientská aplikace nezávisí na webovém rozhraní API.)</span><span class="sxs-lookup"><span data-stu-id="921dd-112">(The example OData service is built using Web API 2, but the client application does not depend on Web API.)</span></span>

<span data-ttu-id="921dd-113">V tomto kurzu Vás provedeme vytvořením klientské aplikace, která volá službu OData.</span><span class="sxs-lookup"><span data-stu-id="921dd-113">In this tutorial, I'll walk through creating a client application that calls an OData service.</span></span> <span data-ttu-id="921dd-114">Služba OData zpřístupňuje následující entity:</span><span class="sxs-lookup"><span data-stu-id="921dd-114">The OData service exposes the following entities:</span></span>

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

<span data-ttu-id="921dd-115">Následující články popisují implementaci služby OData ve webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="921dd-115">The following articles describe how to implement the OData service in Web API.</span></span> <span data-ttu-id="921dd-116">(K pochopení tohoto kurzu ale nemusíte číst.)</span><span class="sxs-lookup"><span data-stu-id="921dd-116">(You don't need to read them to understand this tutorial, however.)</span></span>

- [<span data-ttu-id="921dd-117">Vytvoření koncového bodu OData ve webovém rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="921dd-117">Creating an OData Endpoint in Web API 2</span></span>](creating-an-odata-endpoint.md)
- [<span data-ttu-id="921dd-118">Vztahy entit OData ve webovém rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="921dd-118">OData Entity Relations in Web API 2</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="921dd-119">Akce OData ve webovém rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="921dd-119">OData Actions in Web API 2</span></span>](odata-actions.md)

## <a name="generate-the-service-proxy"></a><span data-ttu-id="921dd-120">Vygenerovat proxy služby</span><span class="sxs-lookup"><span data-stu-id="921dd-120">Generate the Service Proxy</span></span>

<span data-ttu-id="921dd-121">Prvním krokem je vygenerování proxy služby.</span><span class="sxs-lookup"><span data-stu-id="921dd-121">The first step is to generate a service proxy.</span></span> <span data-ttu-id="921dd-122">Proxy služby je třída rozhraní .NET, která definuje metody pro přístup ke službě OData.</span><span class="sxs-lookup"><span data-stu-id="921dd-122">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="921dd-123">Proxy překládá volání metod na požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="921dd-123">The proxy translates method calls into HTTP requests.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

<span data-ttu-id="921dd-124">Začněte otevřením projektu služby OData v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="921dd-124">Start by opening the OData service project in Visual Studio.</span></span> <span data-ttu-id="921dd-125">Stisknutím kombinace kláves CTRL + F5 spusťte službu místně v IIS Express.</span><span class="sxs-lookup"><span data-stu-id="921dd-125">Press CTRL+F5 to run the service locally in IIS Express.</span></span> <span data-ttu-id="921dd-126">Poznamenejte si místní adresu, včetně čísla portu, které Visual Studio přiřadí.</span><span class="sxs-lookup"><span data-stu-id="921dd-126">Note the local address, including the port number that Visual Studio assigns.</span></span> <span data-ttu-id="921dd-127">Tuto adresu budete potřebovat při vytváření proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="921dd-127">You will need this address when you create the proxy.</span></span>

<span data-ttu-id="921dd-128">Potom otevřete jinou instanci aplikace Visual Studio a vytvořte projekt konzolové aplikace.</span><span class="sxs-lookup"><span data-stu-id="921dd-128">Next, open another instance of Visual Studio and create a console application project.</span></span> <span data-ttu-id="921dd-129">Konzolová aplikace bude naše klientská aplikace OData.</span><span class="sxs-lookup"><span data-stu-id="921dd-129">The console application will be our OData client application.</span></span> <span data-ttu-id="921dd-130">(Projekt můžete také přidat ke stejnému řešení jako služba.)</span><span class="sxs-lookup"><span data-stu-id="921dd-130">(You can also add the project to the same solution as the service.)</span></span>

> [!NOTE]
> <span data-ttu-id="921dd-131">Zbývající kroky odkazují na projekt konzoly.</span><span class="sxs-lookup"><span data-stu-id="921dd-131">The remaining steps refer the console project.</span></span>

<span data-ttu-id="921dd-132">V Průzkumník řešení klikněte pravým tlačítkem na **odkazy** a vyberte **Přidat odkaz na službu**.</span><span class="sxs-lookup"><span data-stu-id="921dd-132">In Solution Explorer, right-click **References** and select **Add Service Reference**.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

<span data-ttu-id="921dd-133">V dialogovém okně **Přidat odkaz na službu** zadejte adresu služby OData:</span><span class="sxs-lookup"><span data-stu-id="921dd-133">In the **Add Service Reference** dialog, type the address of the OData service:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

<span data-ttu-id="921dd-134">kde *port* je číslo portu.</span><span class="sxs-lookup"><span data-stu-id="921dd-134">where *port* is the port number.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

<span data-ttu-id="921dd-135">Do možnosti **obor názvů**zadejte "ProductService".</span><span class="sxs-lookup"><span data-stu-id="921dd-135">For **Namespace**, type "ProductService".</span></span> <span data-ttu-id="921dd-136">Tato možnost definuje obor názvů třídy proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="921dd-136">This option defines the namespace of the proxy class.</span></span>

<span data-ttu-id="921dd-137">Klikněte na **Přejít**.</span><span class="sxs-lookup"><span data-stu-id="921dd-137">Click **Go**.</span></span> <span data-ttu-id="921dd-138">Visual Studio přečte dokument metadat OData, ve kterém zjistí entity ve službě.</span><span class="sxs-lookup"><span data-stu-id="921dd-138">Visual Studio reads the OData metadata document to discover the entities in the service.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

<span data-ttu-id="921dd-139">Kliknutím na tlačítko **OK** přidejte třídu proxy do projektu.</span><span class="sxs-lookup"><span data-stu-id="921dd-139">Click **OK** to add the proxy class to your project.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a><span data-ttu-id="921dd-140">Vytvoření instance proxy třídy služby</span><span class="sxs-lookup"><span data-stu-id="921dd-140">Create an Instance of the Service Proxy Class</span></span>

<span data-ttu-id="921dd-141">V rámci metody `Main` vytvořte novou instanci třídy proxy následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="921dd-141">Inside your `Main` method, create a new instance of the proxy class, as follows:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

<span data-ttu-id="921dd-142">Znovu použijte skutečné číslo portu, ve kterém je vaše služba spuštěná.</span><span class="sxs-lookup"><span data-stu-id="921dd-142">Again, use the actual port number where your service is running.</span></span> <span data-ttu-id="921dd-143">Při nasazení služby použijete identifikátor URI živé služby.</span><span class="sxs-lookup"><span data-stu-id="921dd-143">When you deploy your service, you will use the URI of the live service.</span></span> <span data-ttu-id="921dd-144">Nemusíte aktualizovat proxy server.</span><span class="sxs-lookup"><span data-stu-id="921dd-144">You don't need to update the proxy.</span></span>

<span data-ttu-id="921dd-145">Následující kód přidá obslužnou rutinu události, která vytiskne identifikátor URI žádosti do okna konzoly.</span><span class="sxs-lookup"><span data-stu-id="921dd-145">The following code adds an event handler that prints the request URIs to the console window.</span></span> <span data-ttu-id="921dd-146">Tento krok není povinný, ale je zajímavé zobrazit identifikátory URI pro každý dotaz.</span><span class="sxs-lookup"><span data-stu-id="921dd-146">This step isn't required, but it's interesting to see the URIs for each query.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a><span data-ttu-id="921dd-147">Dotazování služby</span><span class="sxs-lookup"><span data-stu-id="921dd-147">Query the Service</span></span>

<span data-ttu-id="921dd-148">Následující kód získá seznam produktů ze služby OData.</span><span class="sxs-lookup"><span data-stu-id="921dd-148">The following code gets the list of products from the OData service.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

<span data-ttu-id="921dd-149">Všimněte si, že nemusíte psát žádný kód pro odeslání požadavku HTTP nebo analýzu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="921dd-149">Notice that you don't need to write any code to send the HTTP request or parse the response.</span></span> <span data-ttu-id="921dd-150">Třída proxy to provede automaticky při vytváření výčtu kolekce `Container.Products` ve smyčce **foreach** .</span><span class="sxs-lookup"><span data-stu-id="921dd-150">The proxy class does this automatically when you enumerate the `Container.Products` collection in the **foreach** loop.</span></span>

<span data-ttu-id="921dd-151">Když aplikaci spustíte, výstup by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="921dd-151">When you run the application, the output should look like the following:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

<span data-ttu-id="921dd-152">Chcete-li získat entitu podle ID, použijte klauzuli `where`.</span><span class="sxs-lookup"><span data-stu-id="921dd-152">To get an entity by ID, use a `where` clause.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

<span data-ttu-id="921dd-153">Pro zbytek tohoto tématu nezobrazujeme celou `Main` funkci, jenom kód potřebný k volání služby.</span><span class="sxs-lookup"><span data-stu-id="921dd-153">For the rest of this topic, I won't show the entire `Main` function, just the code needed to call the service.</span></span>

## <a name="apply-query-options"></a><span data-ttu-id="921dd-154">Použít možnosti dotazu</span><span class="sxs-lookup"><span data-stu-id="921dd-154">Apply Query Options</span></span>

<span data-ttu-id="921dd-155">OData definuje [Možnosti dotazu](../supporting-odata-query-options.md) , které se dají použít k filtrování, řazení, stránkování dat a tak dále.</span><span class="sxs-lookup"><span data-stu-id="921dd-155">OData defines [query options](../supporting-odata-query-options.md) that can be used to filter, sort, page data, and so forth.</span></span> <span data-ttu-id="921dd-156">V proxy službě můžete tyto možnosti použít pomocí různých výrazů LINQ.</span><span class="sxs-lookup"><span data-stu-id="921dd-156">In the service proxy, you can apply these options by using various LINQ expressions.</span></span>

<span data-ttu-id="921dd-157">V této části se zobrazí stručné příklady.</span><span class="sxs-lookup"><span data-stu-id="921dd-157">In this section, I'll show brief examples.</span></span> <span data-ttu-id="921dd-158">Další podrobnosti najdete v tématu věnovaném [hlediskům LINQ (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="921dd-158">For more details, see the topic [LINQ Considerations (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) on MSDN.</span></span>

### <a name="filtering-filter"></a><span data-ttu-id="921dd-159">Filtrování ($filter)</span><span class="sxs-lookup"><span data-stu-id="921dd-159">Filtering ($filter)</span></span>

<span data-ttu-id="921dd-160">Chcete-li filtrovat, použijte klauzuli `where`.</span><span class="sxs-lookup"><span data-stu-id="921dd-160">To filter, use a `where` clause.</span></span> <span data-ttu-id="921dd-161">Následující příklad filtruje podle kategorie produktu.</span><span class="sxs-lookup"><span data-stu-id="921dd-161">The following example filters by product category.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

<span data-ttu-id="921dd-162">Tento kód odpovídá následujícímu dotazu OData.</span><span class="sxs-lookup"><span data-stu-id="921dd-162">This code corresponds to the following OData query.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

<span data-ttu-id="921dd-163">Všimněte si, že proxy převede klauzuli `where` na výraz `$filter` OData.</span><span class="sxs-lookup"><span data-stu-id="921dd-163">Notice that the proxy converts the `where` clause into an OData `$filter` expression.</span></span>

### <a name="sorting-orderby"></a><span data-ttu-id="921dd-164">Řazení ($orderby)</span><span class="sxs-lookup"><span data-stu-id="921dd-164">Sorting ($orderby)</span></span>

<span data-ttu-id="921dd-165">K řazení použijte klauzuli `orderby`.</span><span class="sxs-lookup"><span data-stu-id="921dd-165">To sort, use an `orderby` clause.</span></span> <span data-ttu-id="921dd-166">Následující příklad seřadí podle ceny od nejvyšších po nejnižší.</span><span class="sxs-lookup"><span data-stu-id="921dd-166">The following example sorts by price, from highest to lowest.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

<span data-ttu-id="921dd-167">Zde je odpovídající požadavek OData.</span><span class="sxs-lookup"><span data-stu-id="921dd-167">Here is the corresponding OData request.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a><span data-ttu-id="921dd-168">Stránkování na straně klienta ($skip a $top)</span><span class="sxs-lookup"><span data-stu-id="921dd-168">Client-Side Paging ($skip and $top)</span></span>

<span data-ttu-id="921dd-169">U rozsáhlých sad entit může klient chtít omezit počet výsledků.</span><span class="sxs-lookup"><span data-stu-id="921dd-169">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="921dd-170">Klient může například zobrazit 10 položek najednou.</span><span class="sxs-lookup"><span data-stu-id="921dd-170">For example, a client might show 10 entries at a time.</span></span> <span data-ttu-id="921dd-171">Označuje se jako *stránkování na straně klienta*.</span><span class="sxs-lookup"><span data-stu-id="921dd-171">This is called *client-side paging*.</span></span> <span data-ttu-id="921dd-172">(K dispozici je také [stránkování na straně serveru](../supporting-odata-query-options.md#server-paging), kde server omezuje počet výsledků.) Chcete-li provést stránkování na straně klienta, použijte metody LINQ **Skip** a **probrat** .</span><span class="sxs-lookup"><span data-stu-id="921dd-172">(There is also [server-side paging](../supporting-odata-query-options.md#server-paging), where the server limits the number of results.) To perform client-side paging, use the LINQ **Skip** and **Take** methods.</span></span> <span data-ttu-id="921dd-173">Následující příklad přeskočí prvních 40 výsledků a provede následující 10.</span><span class="sxs-lookup"><span data-stu-id="921dd-173">The following example skips the first 40 results and takes the next 10.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

<span data-ttu-id="921dd-174">Toto je odpovídající požadavek OData:</span><span class="sxs-lookup"><span data-stu-id="921dd-174">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a><span data-ttu-id="921dd-175">Select ($select) a expand ($expand)</span><span class="sxs-lookup"><span data-stu-id="921dd-175">Select ($select) and Expand ($expand)</span></span>

<span data-ttu-id="921dd-176">Chcete-li zahrnout související entity, použijte metodu `DataServiceQuery<t>.Expand`.</span><span class="sxs-lookup"><span data-stu-id="921dd-176">To include related entities, use the `DataServiceQuery<t>.Expand` method.</span></span> <span data-ttu-id="921dd-177">Pokud například chcete zahrnout `Supplier` pro každý `Product`:</span><span class="sxs-lookup"><span data-stu-id="921dd-177">For example, to include the `Supplier` for each `Product`:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

<span data-ttu-id="921dd-178">Toto je odpovídající požadavek OData:</span><span class="sxs-lookup"><span data-stu-id="921dd-178">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

<span data-ttu-id="921dd-179">Chcete-li změnit tvar odpovědi, použijte klauzuli LINQ **Select** .</span><span class="sxs-lookup"><span data-stu-id="921dd-179">To change the shape of the response, use the LINQ **select** clause.</span></span> <span data-ttu-id="921dd-180">Následující příklad získá jenom název každého produktu bez dalších vlastností.</span><span class="sxs-lookup"><span data-stu-id="921dd-180">The following example gets just the name of each product, with no other properties.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

<span data-ttu-id="921dd-181">Toto je odpovídající požadavek OData:</span><span class="sxs-lookup"><span data-stu-id="921dd-181">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

<span data-ttu-id="921dd-182">Klauzule SELECT může zahrnovat související entity.</span><span class="sxs-lookup"><span data-stu-id="921dd-182">A select clause can include related entities.</span></span> <span data-ttu-id="921dd-183">V takovém případě Nevolejte příkaz **expand**; proxy server automaticky obsahuje rozšíření v tomto případě.</span><span class="sxs-lookup"><span data-stu-id="921dd-183">In that case, do not call **Expand**; the proxy automatically includes the expansion in this case.</span></span> <span data-ttu-id="921dd-184">Následující příklad získá název a dodavatel každého produktu.</span><span class="sxs-lookup"><span data-stu-id="921dd-184">The following example gets the name and supplier of each product.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

<span data-ttu-id="921dd-185">Zde je odpovídající požadavek OData.</span><span class="sxs-lookup"><span data-stu-id="921dd-185">Here is the corresponding OData request.</span></span> <span data-ttu-id="921dd-186">Všimněte si, že obsahuje možnost **$expand** .</span><span class="sxs-lookup"><span data-stu-id="921dd-186">Notice that it includes the **$expand** option.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

<span data-ttu-id="921dd-187">Další informace o $select a $expand najdete v tématu [použití $Select, $expand a $Value ve webovém rozhraní API 2](../using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="921dd-187">For more information about $select and $expand, see [Using $select, $expand, and $value in Web API 2](../using-select-expand-and-value.md).</span></span>

## <a name="add-a-new-entity"></a><span data-ttu-id="921dd-188">Přidat novou entitu</span><span class="sxs-lookup"><span data-stu-id="921dd-188">Add a New Entity</span></span>

<span data-ttu-id="921dd-189">Chcete-li přidat novou entitu do sady entit, zavolejte `AddToEntitySet`, kde *EntitySet* je název sady entit.</span><span class="sxs-lookup"><span data-stu-id="921dd-189">To add a new entity to an entity set, call `AddToEntitySet`, where *EntitySet* is the name of the entity set.</span></span> <span data-ttu-id="921dd-190">`AddToProducts` například přidá novou `Product` do sady entit `Products`.</span><span class="sxs-lookup"><span data-stu-id="921dd-190">For example, `AddToProducts` adds a new `Product` to the `Products` entity set.</span></span> <span data-ttu-id="921dd-191">Když vygenerujete proxy server, WCF Data Services automaticky vytvoří tyto metody silného typu **AddTo** .</span><span class="sxs-lookup"><span data-stu-id="921dd-191">When you generate the proxy, WCF Data Services automatically creates these strongly-typed **AddTo** methods.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

<span data-ttu-id="921dd-192">Chcete-li přidat propojení mezi dvěma entitami, použijte metody **addlink** a **SetLink** .</span><span class="sxs-lookup"><span data-stu-id="921dd-192">To add a link between two entities, use the **AddLink** and **SetLink** methods.</span></span> <span data-ttu-id="921dd-193">Následující kód přidá nového dodavatele a nový produkt a vytvoří propojení mezi nimi.</span><span class="sxs-lookup"><span data-stu-id="921dd-193">The following code adds a new supplier and a new product, and then creates links between them.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

<span data-ttu-id="921dd-194">Pokud je navigační vlastnost kolekce, použijte **addlink** .</span><span class="sxs-lookup"><span data-stu-id="921dd-194">Use **AddLink** when the navigation property is a collection.</span></span> <span data-ttu-id="921dd-195">V tomto příkladu přidáme produkt do kolekce `Products` na dodavatele.</span><span class="sxs-lookup"><span data-stu-id="921dd-195">In this example, we are adding a product to the `Products` collection on the supplier.</span></span>

<span data-ttu-id="921dd-196">Pokud je navigační vlastnost jediná entita, použijte **SetLink** .</span><span class="sxs-lookup"><span data-stu-id="921dd-196">Use **SetLink** when the navigation property is a single entity.</span></span> <span data-ttu-id="921dd-197">V tomto příkladu nastavujeme vlastnost `Supplier` v produktu.</span><span class="sxs-lookup"><span data-stu-id="921dd-197">In this example, we are setting the `Supplier` property on the product.</span></span>

## <a name="update--patch"></a><span data-ttu-id="921dd-198">Aktualizovat/opravit</span><span class="sxs-lookup"><span data-stu-id="921dd-198">Update / Patch</span></span>

<span data-ttu-id="921dd-199">Chcete-li aktualizovat entitu, zavolejte metodu **UpdateObject** .</span><span class="sxs-lookup"><span data-stu-id="921dd-199">To update an entity, call the **UpdateObject** method.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

<span data-ttu-id="921dd-200">Aktualizace je provedena při volání **metody SaveChanges**.</span><span class="sxs-lookup"><span data-stu-id="921dd-200">The update is performed when you call **SaveChanges**.</span></span> <span data-ttu-id="921dd-201">Ve výchozím nastavení posílá WCF požadavek na sloučení HTTP.</span><span class="sxs-lookup"><span data-stu-id="921dd-201">By default, WCF sends an HTTP MERGE request.</span></span> <span data-ttu-id="921dd-202">Možnost **PatchOnUpdate** instruuje WCF, aby místo toho odeslal opravu http.</span><span class="sxs-lookup"><span data-stu-id="921dd-202">The **PatchOnUpdate** option tells WCF to send an HTTP PATCH instead.</span></span>

> [!NOTE]
> <span data-ttu-id="921dd-203">Proč je oprava oproti sloučení?</span><span class="sxs-lookup"><span data-stu-id="921dd-203">Why PATCH versus MERGE?</span></span> <span data-ttu-id="921dd-204">Původní specifikace protokolu HTTP 1,1 ([RCF 2616](http://tools.ietf.org/html/rfc2616)) nedefinovala žádnou metodu HTTP se sémantikou "částečná aktualizace".</span><span class="sxs-lookup"><span data-stu-id="921dd-204">The original HTTP 1.1 specification ([RCF 2616](http://tools.ietf.org/html/rfc2616)) did not define any HTTP method with "partial update" semantics.</span></span> <span data-ttu-id="921dd-205">Pro podporu částečných aktualizací specifikace OData definovala metodu sloučení.</span><span class="sxs-lookup"><span data-stu-id="921dd-205">To support partial updates, the OData specification defined the MERGE method.</span></span> <span data-ttu-id="921dd-206">V 2010 se v [RFC 5789](http://tools.ietf.org/html/rfc5789) definovala metoda opravy pro částečné aktualizace.</span><span class="sxs-lookup"><span data-stu-id="921dd-206">In 2010, [RFC 5789](http://tools.ietf.org/html/rfc5789) defined the PATCH method for partial updates.</span></span> <span data-ttu-id="921dd-207">V tomto [příspěvku blogu](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) na blogu WCF Data Services si můžete přečíst některé historie.</span><span class="sxs-lookup"><span data-stu-id="921dd-207">You can read some of the history in this [blog post](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) on the WCF Data Services Blog.</span></span> <span data-ttu-id="921dd-208">V současné době se při sloučení upřednostňuje oprava.</span><span class="sxs-lookup"><span data-stu-id="921dd-208">Today, PATCH is preferred over MERGE.</span></span> <span data-ttu-id="921dd-209">Kontroler OData vytvořený pomocí generování uživatelského rozhraní webového rozhraní API podporuje obě metody.</span><span class="sxs-lookup"><span data-stu-id="921dd-209">The OData controller created by the Web API scaffolding supports both methods.</span></span>

<span data-ttu-id="921dd-210">Pokud chcete nahradit celou entitu (uvést sémantiku), zadejte možnost **ReplaceOnUpdate** .</span><span class="sxs-lookup"><span data-stu-id="921dd-210">If you want to replace the entire entity (PUT semantics), specify the **ReplaceOnUpdate** option.</span></span> <span data-ttu-id="921dd-211">To způsobí, že WCF odešle požadavek HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="921dd-211">This causes WCF to send an HTTP PUT request.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a><span data-ttu-id="921dd-212">Odstranění entity</span><span class="sxs-lookup"><span data-stu-id="921dd-212">Delete an Entity</span></span>

<span data-ttu-id="921dd-213">Pokud chcete entitu odstranit, zavolejte na **OdstranitObjekt**.</span><span class="sxs-lookup"><span data-stu-id="921dd-213">To delete an entity, call **DeleteObject**.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a><span data-ttu-id="921dd-214">Vyvolat akci OData</span><span class="sxs-lookup"><span data-stu-id="921dd-214">Invoke an OData Action</span></span>

<span data-ttu-id="921dd-215">V OData představují [Akce](odata-actions.md) způsob, jak přidat chování na straně serveru, které není snadno definované jako operace CRUD u entit.</span><span class="sxs-lookup"><span data-stu-id="921dd-215">In OData, [actions](odata-actions.md) are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span>

<span data-ttu-id="921dd-216">I když dokument metadat OData popisuje akce, Třída proxy nevytváří pro ně žádné metody silného typu.</span><span class="sxs-lookup"><span data-stu-id="921dd-216">Although the OData metadata document describes the actions, the proxy class does not create any strongly-typed methods for them.</span></span> <span data-ttu-id="921dd-217">Můžete přesto vyvolat akci OData pomocí obecné metody **Execute** .</span><span class="sxs-lookup"><span data-stu-id="921dd-217">You can still invoke an OData action by using the generic **Execute** method.</span></span> <span data-ttu-id="921dd-218">Budete ale muset znát datové typy parametrů a vrácenou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="921dd-218">However, you will need to know the data types of the parameters and the return value.</span></span>

<span data-ttu-id="921dd-219">Například akce `RateProduct` přijímá parametr s názvem "hodnocení" typu `Int32` a vrátí `double`.</span><span class="sxs-lookup"><span data-stu-id="921dd-219">For example, the `RateProduct` action takes parameter named "Rating" of type `Int32` and returns a `double`.</span></span> <span data-ttu-id="921dd-220">Následující kód ukazuje, jak tuto akci vyvolat.</span><span class="sxs-lookup"><span data-stu-id="921dd-220">The following code shows how to invoke this action.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

<span data-ttu-id="921dd-221">Další informace najdete v tématu[volání operací a akcí služby](https://msdn.microsoft.com/library/hh230677.aspx).</span><span class="sxs-lookup"><span data-stu-id="921dd-221">For more information, see[Calling Service Operations and Actions](https://msdn.microsoft.com/library/hh230677.aspx).</span></span>

<span data-ttu-id="921dd-222">Jednou z možností je zvětšit třídu **kontejneru** tak, aby poskytovala metodu silného typu, která vyvolá tuto akci:</span><span class="sxs-lookup"><span data-stu-id="921dd-222">One option is to extend the **Container** class to provide a strongly typed method that invokes the action:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
