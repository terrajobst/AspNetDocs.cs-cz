---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: Řadiče testování částí v ASP.NET webovém rozhraní API 2 | Microsoft Docs
author: MikeWasson
description: Toto téma popisuje některé konkrétní techniky pro řadiče testování částí ve webovém rozhraní API 2. Než si přečtete toto téma, možná budete chtít přečíst jednotku kurzu...
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: cdb1700537021e276669de1a9e0330a62659746c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554990"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a><span data-ttu-id="c6acf-104">Testování jednotek kontrolerů webového rozhraní API 2 technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c6acf-104">Unit Testing Controllers in ASP.NET Web API 2</span></span>

<span data-ttu-id="c6acf-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c6acf-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="c6acf-106">Toto téma popisuje některé konkrétní techniky pro řadiče testování částí ve webovém rozhraní API 2.</span><span class="sxs-lookup"><span data-stu-id="c6acf-106">This topic describes some specific techniques for unit testing controllers in Web API 2.</span></span> <span data-ttu-id="c6acf-107">Než si přečtete toto téma, možná budete chtít přečíst kurz [testování částí ASP.NET webového rozhraní API 2](unit-testing-with-aspnet-web-api.md), které ukazuje, jak do řešení přidat projekt testování částí.</span><span class="sxs-lookup"><span data-stu-id="c6acf-107">Before reading this topic, you might want to read the tutorial [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), which shows how to add a unit-test project to your solution.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c6acf-108">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="c6acf-108">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="c6acf-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6acf-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="c6acf-110">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="c6acf-110">Web API 2</span></span>
> - <span data-ttu-id="c6acf-111">[MOQ](https://github.com/Moq) 4.5.30</span><span class="sxs-lookup"><span data-stu-id="c6acf-111">[Moq](https://github.com/Moq) 4.5.30</span></span>

> [!NOTE]
> <span data-ttu-id="c6acf-112">Použil (a) jsem MOQ, ale stejný nápad se vztahuje i na jakékoli makety rozhraní.</span><span class="sxs-lookup"><span data-stu-id="c6acf-112">I used Moq, but the same idea applies to any mocking framework.</span></span> <span data-ttu-id="c6acf-113">MOQ 4.5.30 (a novější) podporuje sady Visual Studio 2017, Roslyn a .NET 4,5 a novější verze.</span><span class="sxs-lookup"><span data-stu-id="c6acf-113">Moq 4.5.30 (and later) supports Visual Studio 2017, Roslyn and .NET 4.5 and later versions.</span></span>

<span data-ttu-id="c6acf-114">Běžným vzorem při testování částí je &quot;příkaz Uspořádat-Act-Assert&quot;:</span><span class="sxs-lookup"><span data-stu-id="c6acf-114">A common pattern in unit tests is &quot;arrange-act-assert&quot;:</span></span>

- <span data-ttu-id="c6acf-115">Uspořádat: nastavte všechny požadované součásti pro spuštění testu.</span><span class="sxs-lookup"><span data-stu-id="c6acf-115">Arrange: Set up any prerequisites for the test to run.</span></span>
- <span data-ttu-id="c6acf-116">ACT: proveďte test.</span><span class="sxs-lookup"><span data-stu-id="c6acf-116">Act: Perform the test.</span></span>
- <span data-ttu-id="c6acf-117">Assert: Ověřte, že test proběhl úspěšně.</span><span class="sxs-lookup"><span data-stu-id="c6acf-117">Assert: Verify that the test succeeded.</span></span>

<span data-ttu-id="c6acf-118">V kroku uspořádat často použijete objekty s přípravou nebo se zástupnými procedurami.</span><span class="sxs-lookup"><span data-stu-id="c6acf-118">In the arrange step, you will often use mock or stub objects.</span></span> <span data-ttu-id="c6acf-119">Který minimalizuje počet závislostí, takže se test zaměřuje na testování jedné věci.</span><span class="sxs-lookup"><span data-stu-id="c6acf-119">That minimizes the number of dependencies, so the test is focused on testing one thing.</span></span>

<span data-ttu-id="c6acf-120">Tady je několik věcí, které byste měli testovat jednotkou v řadičích webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="c6acf-120">Here are some things that you should unit test in your Web API controllers:</span></span>

- <span data-ttu-id="c6acf-121">Akce vrátí správný typ odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c6acf-121">The action returns the correct type of response.</span></span>
- <span data-ttu-id="c6acf-122">Neplatné parametry vracejí správnou chybovou odpověď.</span><span class="sxs-lookup"><span data-stu-id="c6acf-122">Invalid parameters return the correct error response.</span></span>
- <span data-ttu-id="c6acf-123">Akce volá správnou metodu pro úložiště nebo vrstvu služby.</span><span class="sxs-lookup"><span data-stu-id="c6acf-123">The action calls the correct method on the repository or service layer.</span></span>
- <span data-ttu-id="c6acf-124">Pokud odpověď obsahuje doménový model, ověřte typ modelu.</span><span class="sxs-lookup"><span data-stu-id="c6acf-124">If the response includes a domain model, verify the model type.</span></span>

<span data-ttu-id="c6acf-125">Jedná se o některé obecné věci, které je potřeba otestovat, ale konkrétní závisí na vaší implementaci kontroleru.</span><span class="sxs-lookup"><span data-stu-id="c6acf-125">These are some of the general things to test, but the specifics depend on your controller implementation.</span></span> <span data-ttu-id="c6acf-126">Konkrétně se jedná o velký rozdíl, zda akce kontroleru vrátí **HttpResponseMessage** nebo **IHttpActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c6acf-126">In particular, it makes a big difference whether your controller actions return **HttpResponseMessage** or **IHttpActionResult**.</span></span> <span data-ttu-id="c6acf-127">Další informace o těchto typech výsledků najdete v tématu [výsledky akcí ve webovém rozhraní API 2](../getting-started-with-aspnet-web-api/action-results.md).</span><span class="sxs-lookup"><span data-stu-id="c6acf-127">For more information about these result types, see [Action Results in Web Api 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

## <a name="testing-actions-that-return-httpresponsemessage"></a><span data-ttu-id="c6acf-128">Testování akcí, které vracejí HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="c6acf-128">Testing Actions that Return HttpResponseMessage</span></span>

<span data-ttu-id="c6acf-129">Tady je příklad kontroleru, jehož akce vrací **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="c6acf-129">Here is an example of a controller whose actions return **HttpResponseMessage**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

<span data-ttu-id="c6acf-130">Všimněte si, že kontroler používá vkládání závislostí pro vložení `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="c6acf-130">Notice the controller uses dependency injection to inject an `IProductRepository`.</span></span> <span data-ttu-id="c6acf-131">Tím se kontroler testovatelné, protože můžete vložit maketu úložiště.</span><span class="sxs-lookup"><span data-stu-id="c6acf-131">That makes the controller more testable, because you can inject a mock repository.</span></span> <span data-ttu-id="c6acf-132">Následující test jednotky ověřuje, že metoda `Get` zapisuje `Product` do těla odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c6acf-132">The following unit test verifies that the `Get` method writes a `Product` to the response body.</span></span> <span data-ttu-id="c6acf-133">Předpokládejme, že `repository` je `IProductRepository`typu.</span><span class="sxs-lookup"><span data-stu-id="c6acf-133">Assume that `repository` is a mock `IProductRepository`.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

<span data-ttu-id="c6acf-134">Je důležité nastavit na řadiči **požadavek** a **konfiguraci** .</span><span class="sxs-lookup"><span data-stu-id="c6acf-134">It's important to set **Request** and **Configuration** on the controller.</span></span> <span data-ttu-id="c6acf-135">V opačném případě se test nezdaří s **ArgumentNullException** nebo **InvalidOperationException**.</span><span class="sxs-lookup"><span data-stu-id="c6acf-135">Otherwise, the test will fail with an **ArgumentNullException** or **InvalidOperationException**.</span></span>

## <a name="testing-link-generation"></a><span data-ttu-id="c6acf-136">Testování generování odkazů</span><span class="sxs-lookup"><span data-stu-id="c6acf-136">Testing Link Generation</span></span>

<span data-ttu-id="c6acf-137">Metoda `Post` volá **UrlHelper. Link** a vytvoří odkazy v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c6acf-137">The `Post` method calls **UrlHelper.Link** to create links in the response.</span></span> <span data-ttu-id="c6acf-138">K tomu je potřeba pár dalších nastavení v testu jednotek:</span><span class="sxs-lookup"><span data-stu-id="c6acf-138">This requires a little more setup in the unit test:</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

<span data-ttu-id="c6acf-139">Třída **UrlHelper** potřebuje adresu URL požadavku a data směrování, takže test musí nastavovat hodnoty pro tyto.</span><span class="sxs-lookup"><span data-stu-id="c6acf-139">The **UrlHelper** class needs the request URL and route data, so the test has to set values for these.</span></span> <span data-ttu-id="c6acf-140">Další možností je **UrlHelper**nebo zástupné procedury.</span><span class="sxs-lookup"><span data-stu-id="c6acf-140">Another option is mock or stub **UrlHelper**.</span></span> <span data-ttu-id="c6acf-141">S tímto přístupem nahradíte výchozí hodnotu [ApiController. URL](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) s použitím přípravné nebo zástupné verze, která vrací pevnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="c6acf-141">With this approach, you replace the default value of [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) with a mock or stub version that returns a fixed value.</span></span>

<span data-ttu-id="c6acf-142">Pojďme přepsat test pomocí [MOQ](https://github.com/Moq) Frameworku.</span><span class="sxs-lookup"><span data-stu-id="c6acf-142">Let's rewrite the test using the [Moq](https://github.com/Moq) framework.</span></span> <span data-ttu-id="c6acf-143">Nainstalujte balíček NuGet `Moq` do testovacího projektu.</span><span class="sxs-lookup"><span data-stu-id="c6acf-143">Install the `Moq` NuGet package in the test project.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

<span data-ttu-id="c6acf-144">V této verzi nemusíte nastavovat žádná data trasy, protože **UrlHelper** typu vrátí konstantní řetězec.</span><span class="sxs-lookup"><span data-stu-id="c6acf-144">In this version, you don't need to set up any route data, because the mock **UrlHelper** returns a constant string.</span></span>

## <a name="testing-actions-that-return-ihttpactionresult"></a><span data-ttu-id="c6acf-145">Testování akcí, které vracejí IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="c6acf-145">Testing Actions that Return IHttpActionResult</span></span>

<span data-ttu-id="c6acf-146">Ve webovém rozhraní API 2 může akce kontroleru vracet **IHttpActionResult**, což je obdobou **ACTIONRESULT** ve ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c6acf-146">In Web API 2, a controller action can return **IHttpActionResult**, which is analogous to **ActionResult** in ASP.NET MVC.</span></span> <span data-ttu-id="c6acf-147">Rozhraní **IHttpActionResult** definuje vzor příkazu pro vytváření odpovědí HTTP.</span><span class="sxs-lookup"><span data-stu-id="c6acf-147">The **IHttpActionResult** interface defines a command pattern for creating HTTP responses.</span></span> <span data-ttu-id="c6acf-148">Místo přímého vytvoření odpovědi kontroler vrátí **IHttpActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c6acf-148">Instead of creating the response directly, the controller returns an **IHttpActionResult**.</span></span> <span data-ttu-id="c6acf-149">Později kanál vyvolá **IHttpActionResult** , aby vytvořil odpověď.</span><span class="sxs-lookup"><span data-stu-id="c6acf-149">Later, the pipeline invokes the **IHttpActionResult** to create the response.</span></span> <span data-ttu-id="c6acf-150">Tento přístup usnadňuje psaní jednotkových testů, protože můžete přeskočit spoustu nastavení, které je potřeba pro **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="c6acf-150">This approach makes it easier to write unit tests, because you can skip a lot of the setup that is needed for **HttpResponseMessage**.</span></span>

<span data-ttu-id="c6acf-151">Tady je příklad kontroleru, jehož akce vrací **IHttpActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c6acf-151">Here is an example controller whose actions return **IHttpActionResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

<span data-ttu-id="c6acf-152">Tento příklad ukazuje některé běžné vzory pomocí **IHttpActionResult**.</span><span class="sxs-lookup"><span data-stu-id="c6acf-152">This example shows some common patterns using **IHttpActionResult**.</span></span> <span data-ttu-id="c6acf-153">Pojďme se podívat, jak je zkoušet jednotkou.</span><span class="sxs-lookup"><span data-stu-id="c6acf-153">Let's see how to unit test them.</span></span>

### <a name="action-returns-200-ok-with-a-response-body"></a><span data-ttu-id="c6acf-154">Akce vrátí 200 (OK) s textem odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c6acf-154">Action returns 200 (OK) with a response body</span></span>

<span data-ttu-id="c6acf-155">Metoda `Get` volá `Ok(product)`, pokud se produkt najde.</span><span class="sxs-lookup"><span data-stu-id="c6acf-155">The `Get` method calls `Ok(product)` if the product is found.</span></span> <span data-ttu-id="c6acf-156">V testu jednotek se ujistěte, že je návratový typ **OkNegotiatedContentResult** a vrácený produkt má správné ID.</span><span class="sxs-lookup"><span data-stu-id="c6acf-156">In the unit test, make sure the return type is **OkNegotiatedContentResult** and the returned product has the right ID.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

<span data-ttu-id="c6acf-157">Všimněte si, že test jednotky neprovede výsledek akce.</span><span class="sxs-lookup"><span data-stu-id="c6acf-157">Notice that the unit test doesn't execute the action result.</span></span> <span data-ttu-id="c6acf-158">Můžete předpokládat, že výsledek akce vytvoří odpověď HTTP správně.</span><span class="sxs-lookup"><span data-stu-id="c6acf-158">You can assume the action result creates the HTTP response correctly.</span></span> <span data-ttu-id="c6acf-159">(To je důvod, proč rozhraní Web API má vlastní testy jednotek!)</span><span class="sxs-lookup"><span data-stu-id="c6acf-159">(That's why the Web API framework has its own unit tests!)</span></span>

### <a name="action-returns-404-not-found"></a><span data-ttu-id="c6acf-160">Akce vrátí 404 (Nenalezeno).</span><span class="sxs-lookup"><span data-stu-id="c6acf-160">Action returns 404 (Not Found)</span></span>

<span data-ttu-id="c6acf-161">Metoda `Get` volá `NotFound()`, pokud produkt nenalezne.</span><span class="sxs-lookup"><span data-stu-id="c6acf-161">The `Get` method calls `NotFound()` if the product is not found.</span></span> <span data-ttu-id="c6acf-162">Pro tento případ test jednotek pouze kontroluje, zda je návratový typ **NotFoundResult**.</span><span class="sxs-lookup"><span data-stu-id="c6acf-162">For this case, the unit test just checks if the return type is **NotFoundResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a><span data-ttu-id="c6acf-163">Akce vrátí 200 (OK) bez textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c6acf-163">Action returns 200 (OK) with no response body</span></span>

<span data-ttu-id="c6acf-164">Metoda `Delete` volá `Ok()`, aby vrátila prázdnou odpověď HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="c6acf-164">The `Delete` method calls `Ok()` to return an empty HTTP 200 response.</span></span> <span data-ttu-id="c6acf-165">Podobně jako v předchozím příkladu test jednotek kontroluje návratový typ, v tomto případě **OkResult**.</span><span class="sxs-lookup"><span data-stu-id="c6acf-165">Like the previous example, the unit test checks the return type, in this case **OkResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a><span data-ttu-id="c6acf-166">Akce vrátí 201 (vytvořeno) s hlavičkou umístění.</span><span class="sxs-lookup"><span data-stu-id="c6acf-166">Action returns 201 (Created) with a Location header</span></span>

<span data-ttu-id="c6acf-167">Metoda `Post` volá `CreatedAtRoute`, aby vrátila odpověď HTTP 201 s identifikátorem URI v hlavičce umístění.</span><span class="sxs-lookup"><span data-stu-id="c6acf-167">The `Post` method calls `CreatedAtRoute` to return an HTTP 201 response with a URI in the Location header.</span></span> <span data-ttu-id="c6acf-168">V testu jednotky ověřte, zda akce nastavuje správné hodnoty směrování.</span><span class="sxs-lookup"><span data-stu-id="c6acf-168">In the unit test, verify that the action sets the correct routing values.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a><span data-ttu-id="c6acf-169">Akce vrátí jiný 2xx s textem odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c6acf-169">Action returns another 2xx with a response body</span></span>

<span data-ttu-id="c6acf-170">Metoda `Put` volá `Content`, aby vrátila odpověď HTTP 202 (přijato) s textem odpovědi.</span><span class="sxs-lookup"><span data-stu-id="c6acf-170">The `Put` method calls `Content` to return an HTTP 202 (Accepted) response with a response body.</span></span> <span data-ttu-id="c6acf-171">Tento případ je podobný jako vracení 200 (OK), ale test jednotky by také měl zkontrolovat stavový kód.</span><span class="sxs-lookup"><span data-stu-id="c6acf-171">This case is similar to returning 200 (OK), but the unit test should also check the status code.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="c6acf-172">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="c6acf-172">Additional Resources</span></span>

- [<span data-ttu-id="c6acf-173">Napodobování Entity Framework při testování jednotek webového rozhraní API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c6acf-173">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- <span data-ttu-id="c6acf-174">[Zápis testů pro službu ASP.NET Web API](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (Blogový příspěvek – Youssef Moussaoui).</span><span class="sxs-lookup"><span data-stu-id="c6acf-174">[Writing tests for an ASP.NET Web API service](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (blog post by Youssef Moussaoui).</span></span>
- [<span data-ttu-id="c6acf-175">Ladění webového rozhraní API ASP.NET pomocí ladicího programu směrování</span><span class="sxs-lookup"><span data-stu-id="c6acf-175">Debugging ASP.NET Web API with Route Debugger</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
