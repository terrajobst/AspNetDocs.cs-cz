---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Výsledky akcí ve webovém rozhraní API 2 – ASP.NET 4.x
author: MikeWasson
description: Popisuje, jak rozhraní ASP.NET Web API převede návratovou hodnotu z akce kontroleru do zpráva s odpovědí HTTP v technologii ASP.NET 4.x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 87f71938a5c5f38d3a456ba9339540f67e236e1a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400890"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="27b19-103">Výsledky akcí ve webovém rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="27b19-103">Action Results in Web API 2</span></span>

<span data-ttu-id="27b19-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="27b19-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="27b19-105">Toto téma popisuje, jak rozhraní ASP.NET Web API převede návratovou hodnotu z akce kontroleru do zprávy s odpovědí HTTP.</span><span class="sxs-lookup"><span data-stu-id="27b19-105">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="27b19-106">Akce kontroleru webového rozhraní API může vrátit kterýkoli z následujících:</span><span class="sxs-lookup"><span data-stu-id="27b19-106">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="27b19-107">void</span><span class="sxs-lookup"><span data-stu-id="27b19-107">void</span></span>
2. **<span data-ttu-id="27b19-108">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="27b19-108">HttpResponseMessage</span></span>**
3. **<span data-ttu-id="27b19-109">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="27b19-109">IHttpActionResult</span></span>**
4. <span data-ttu-id="27b19-110">Jiný typ</span><span class="sxs-lookup"><span data-stu-id="27b19-110">Some other type</span></span>

<span data-ttu-id="27b19-111">Podle toho, která z nich je vrácena, webové rozhraní API k vytvoření odpovědi HTTP používá jiný mechanismus.</span><span class="sxs-lookup"><span data-stu-id="27b19-111">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="27b19-112">Návratový typ</span><span class="sxs-lookup"><span data-stu-id="27b19-112">Return type</span></span> | <span data-ttu-id="27b19-113">Způsob, jak vytvořit webové rozhraní API odpovědi</span><span class="sxs-lookup"><span data-stu-id="27b19-113">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="27b19-114">void</span><span class="sxs-lookup"><span data-stu-id="27b19-114">void</span></span> | <span data-ttu-id="27b19-115">Vrátí prázdný 204 (žádný obsah)</span><span class="sxs-lookup"><span data-stu-id="27b19-115">Return empty 204 (No Content)</span></span> |
| **<span data-ttu-id="27b19-116">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="27b19-116">HttpResponseMessage</span></span>** | <span data-ttu-id="27b19-117">Převeďte přímo na zprávy s odpovědí HTTP.</span><span class="sxs-lookup"><span data-stu-id="27b19-117">Convert directly to an HTTP response message.</span></span> |
| **<span data-ttu-id="27b19-118">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="27b19-118">IHttpActionResult</span></span>** | <span data-ttu-id="27b19-119">Volání **ExecuteAsync** k vytvoření **objekt HttpResponseMessage**, převeďte do zprávy s odpovědí HTTP.</span><span class="sxs-lookup"><span data-stu-id="27b19-119">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="27b19-120">Jiný typ</span><span class="sxs-lookup"><span data-stu-id="27b19-120">Other type</span></span> | <span data-ttu-id="27b19-121">Zápis serializovaná návratovou hodnotu do datové části odpovědi; Vrátí 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="27b19-121">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="27b19-122">Zbývající část tohoto tématu popisuje jednotlivé možnosti podrobněji.</span><span class="sxs-lookup"><span data-stu-id="27b19-122">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="27b19-123">void</span><span class="sxs-lookup"><span data-stu-id="27b19-123">void</span></span>

<span data-ttu-id="27b19-124">Pokud je návratový typ `void`, webové rozhraní API jednoduše vrátí prázdnou odpověď HTTP se stavovým kódem 204 (žádný obsah).</span><span class="sxs-lookup"><span data-stu-id="27b19-124">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="27b19-125">Příklad kontroleru:</span><span class="sxs-lookup"><span data-stu-id="27b19-125">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="27b19-126">Odpověď HTTP:</span><span class="sxs-lookup"><span data-stu-id="27b19-126">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="27b19-127">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="27b19-127">HttpResponseMessage</span></span>

<span data-ttu-id="27b19-128">Pokud tato akce vrátí [objekt HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), webového rozhraní API převede návratovou hodnotu přímo do zprávu odpovědi HTTP pomocí vlastnosti **objekt HttpResponseMessage** objekt pro naplnění odpověď.</span><span class="sxs-lookup"><span data-stu-id="27b19-128">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="27b19-129">Tato možnost poskytuje velké množství kontrolu nad zprávy s odpovědí.</span><span class="sxs-lookup"><span data-stu-id="27b19-129">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="27b19-130">Například následující akce kontroleru nastaví hlavičku Cache-Control.</span><span class="sxs-lookup"><span data-stu-id="27b19-130">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="27b19-131">Odpověď:</span><span class="sxs-lookup"><span data-stu-id="27b19-131">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="27b19-132">Pokud předáte do modelu domény **CreateResponse** metodu, pomocí webového rozhraní API [formátovací modul médií](../formats-and-model-binding/media-formatters.md) zapsat serializovaný model do datové části odpovědi.</span><span class="sxs-lookup"><span data-stu-id="27b19-132">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="27b19-133">Webové rozhraní API používá hlavičky Accept v požadavku k výběru formátovacího modulu.</span><span class="sxs-lookup"><span data-stu-id="27b19-133">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="27b19-134">Další informace najdete v tématu [vyjednávání obsahu](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="27b19-134">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="27b19-135">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="27b19-135">IHttpActionResult</span></span>

<span data-ttu-id="27b19-136">**IHttpActionResult** rozhraní byl zaveden ve webovém rozhraní API 2.</span><span class="sxs-lookup"><span data-stu-id="27b19-136">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="27b19-137">V podstatě definuje **objekt HttpResponseMessage** objekt pro vytváření.</span><span class="sxs-lookup"><span data-stu-id="27b19-137">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="27b19-138">Tady jsou některé výhody použití **IHttpActionResult** rozhraní:</span><span class="sxs-lookup"><span data-stu-id="27b19-138">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="27b19-139">Zjednodušuje [testování částí](../testing-and-debugging/unit-testing-controllers-in-web-api.md) řadičů.</span><span class="sxs-lookup"><span data-stu-id="27b19-139">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="27b19-140">Přesune běžné logiku pro vytváření odpovědí HTTP na samostatné třídy.</span><span class="sxs-lookup"><span data-stu-id="27b19-140">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="27b19-141">Díky záměr jasnější, akce kontroleru skrytím nízké úrovně podrobnosti o vytváření odpovědi.</span><span class="sxs-lookup"><span data-stu-id="27b19-141">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="27b19-142">**IHttpActionResult** obsahuje jedinou metodu **ExecuteAsync**, který asynchronně vytvoří **objekt HttpResponseMessage** instance.</span><span class="sxs-lookup"><span data-stu-id="27b19-142">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="27b19-143">Akce kontroleru vrátí-li **IHttpActionResult**, volá webové rozhraní API **ExecuteAsync** metodu pro vytvoření **objekt HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="27b19-143">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="27b19-144">Potom převede **objekt HttpResponseMessage** do zprávy s odpovědí HTTP.</span><span class="sxs-lookup"><span data-stu-id="27b19-144">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="27b19-145">Tady je jednoduchá implementace **IHttpActionResult** , který vytváří ve formátu prostého textu odpovědi:</span><span class="sxs-lookup"><span data-stu-id="27b19-145">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="27b19-146">Příklad akce kontroleru:</span><span class="sxs-lookup"><span data-stu-id="27b19-146">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="27b19-147">Odpověď:</span><span class="sxs-lookup"><span data-stu-id="27b19-147">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="27b19-148">Častěji, použije **IHttpActionResult** implementace, které jsou definovány v **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** oboru názvů.</span><span class="sxs-lookup"><span data-stu-id="27b19-148">More often, you will use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="27b19-149">**Objektu ApiController** třída definuje pomocné metody, které vracejí výsledky těchto předdefinovaných akcí.</span><span class="sxs-lookup"><span data-stu-id="27b19-149">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="27b19-150">V následujícím příkladu, pokud požadavku se neshoduje s ID existujícího produktu, zavolá kontroleru [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) pro vytvoření odpovědi 404 (Nenalezeno).</span><span class="sxs-lookup"><span data-stu-id="27b19-150">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="27b19-151">Jinak kontroler volá [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), vytváří se odpověď 200 (OK), který obsahuje produktu.</span><span class="sxs-lookup"><span data-stu-id="27b19-151">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="27b19-152">Jiné návratové typy</span><span class="sxs-lookup"><span data-stu-id="27b19-152">Other Return Types</span></span>

<span data-ttu-id="27b19-153">Pro všechny ostatní návratové typy webového rozhraní API používá [formátovací modul médií](../formats-and-model-binding/media-formatters.md) k serializaci návratovou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="27b19-153">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="27b19-154">Webové rozhraní API zapíše serializované hodnoty do datové části odpovědi.</span><span class="sxs-lookup"><span data-stu-id="27b19-154">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="27b19-155">Stavový kód odpovědi je 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="27b19-155">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="27b19-156">Nevýhody tohoto přístupu je, že se nedá vrátit přímo kód chyby, jako je například 404.</span><span class="sxs-lookup"><span data-stu-id="27b19-156">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="27b19-157">Však může vrátit **HttpResponseException** pro kódy chyb.</span><span class="sxs-lookup"><span data-stu-id="27b19-157">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="27b19-158">Další informace najdete v tématu [zpracování výjimek v rozhraní ASP.NET Web API](../error-handling/exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="27b19-158">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="27b19-159">Webové rozhraní API používá hlavičky Accept v požadavku k výběru formátovacího modulu.</span><span class="sxs-lookup"><span data-stu-id="27b19-159">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="27b19-160">Další informace najdete v tématu [vyjednávání obsahu](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="27b19-160">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="27b19-161">Příklad žádosti</span><span class="sxs-lookup"><span data-stu-id="27b19-161">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="27b19-162">Příklad odpovědi:</span><span class="sxs-lookup"><span data-stu-id="27b19-162">Example response:</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
