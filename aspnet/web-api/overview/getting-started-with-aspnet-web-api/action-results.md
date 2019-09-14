---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Výsledek akce ve webovém rozhraní API 2 – ASP.NET 4. x
author: MikeWasson
description: Popisuje způsob, jakým webové rozhraní API ASP.NET převádí návratovou hodnotu z akce kontroleru na zprávu odpovědi HTTP v ASP.NET 4. x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: f00ac0db453053e53d6d6942dd1557b409f4167b
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985836"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="e940c-103">Výsledky akcí ve webovém rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="e940c-103">Action Results in Web API 2</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="e940c-104">Toto téma popisuje, jak webové rozhraní API ASP.NET převádí návratovou hodnotu z akce kontroleru na zprávu HTTP Response.</span><span class="sxs-lookup"><span data-stu-id="e940c-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="e940c-105">Akce kontroleru webového rozhraní API může vracet následující:</span><span class="sxs-lookup"><span data-stu-id="e940c-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="e940c-106">void</span><span class="sxs-lookup"><span data-stu-id="e940c-106">void</span></span>
2. <span data-ttu-id="e940c-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="e940c-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="e940c-108">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="e940c-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="e940c-109">Nějaký jiný typ</span><span class="sxs-lookup"><span data-stu-id="e940c-109">Some other type</span></span>

<span data-ttu-id="e940c-110">V závislosti na tom, které z těchto funkcí se vrátí, webové rozhraní API použije jiný mechanismus k vytvoření odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="e940c-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="e940c-111">Návratový typ</span><span class="sxs-lookup"><span data-stu-id="e940c-111">Return type</span></span> | <span data-ttu-id="e940c-112">Způsob, jakým webové rozhraní API vytvoří odpověď</span><span class="sxs-lookup"><span data-stu-id="e940c-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="e940c-113">void</span><span class="sxs-lookup"><span data-stu-id="e940c-113">void</span></span> | <span data-ttu-id="e940c-114">Vrátit prázdné číslo 204 (žádný obsah)</span><span class="sxs-lookup"><span data-stu-id="e940c-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="e940c-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="e940c-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="e940c-116">Převeďte přímo na zprávu odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="e940c-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="e940c-117">**IHttpActionResult**</span><span class="sxs-lookup"><span data-stu-id="e940c-117">**IHttpActionResult**</span></span> | <span data-ttu-id="e940c-118">Voláním **metody ExecuteAsync** vytvořte **HttpResponseMessage**a pak proveďte převod na zprávu odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="e940c-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="e940c-119">Jiný typ</span><span class="sxs-lookup"><span data-stu-id="e940c-119">Other type</span></span> | <span data-ttu-id="e940c-120">Zapsat serializovanou návratovou hodnotu do těla odpovědi; Vrátí 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="e940c-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="e940c-121">Zbývající část tohoto tématu popisuje jednotlivé možnosti podrobněji.</span><span class="sxs-lookup"><span data-stu-id="e940c-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="e940c-122">void</span><span class="sxs-lookup"><span data-stu-id="e940c-122">void</span></span>

<span data-ttu-id="e940c-123">Pokud je `void`návratový typ, webové rozhraní API jednoduše vrátí prázdnou odpověď HTTP se stavovým kódem 204 (žádný obsah).</span><span class="sxs-lookup"><span data-stu-id="e940c-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="e940c-124">Příklad kontroleru:</span><span class="sxs-lookup"><span data-stu-id="e940c-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="e940c-125">Odpověď HTTP:</span><span class="sxs-lookup"><span data-stu-id="e940c-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="e940c-126">HttpResponseMessage</span><span class="sxs-lookup"><span data-stu-id="e940c-126">HttpResponseMessage</span></span>

<span data-ttu-id="e940c-127">Pokud akce vrátí [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), webové rozhraní API převede návratovou hodnotu přímo do zprávy odpovědi HTTP pomocí vlastností objektu **HttpResponseMessage** k naplnění odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e940c-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="e940c-128">Tato možnost vám poskytne velkou kontrolu nad zprávou odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e940c-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="e940c-129">Například následující akce kontroleru nastaví hlavičku Cache-Control.</span><span class="sxs-lookup"><span data-stu-id="e940c-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="e940c-130">Základě</span><span class="sxs-lookup"><span data-stu-id="e940c-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="e940c-131">Pokud předáte doménový model metodě **CreateResponse** , webové rozhraní API pomocí [formátovacího modulu médií](../formats-and-model-binding/media-formatters.md) zapíše serializovaný model do těla odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e940c-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="e940c-132">Webové rozhraní API používá k výběru formátovacího modulu hlavičku Accept v žádosti.</span><span class="sxs-lookup"><span data-stu-id="e940c-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="e940c-133">Další informace najdete v tématu [vyjednávání obsahu](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="e940c-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="e940c-134">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="e940c-134">IHttpActionResult</span></span>

<span data-ttu-id="e940c-135">Rozhraní **IHttpActionResult** bylo zavedeno ve webovém rozhraní API 2.</span><span class="sxs-lookup"><span data-stu-id="e940c-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="e940c-136">V podstatě definuje objekt pro vytváření **HttpResponseMessage** .</span><span class="sxs-lookup"><span data-stu-id="e940c-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="e940c-137">Zde jsou některé výhody použití rozhraní **IHttpActionResult** :</span><span class="sxs-lookup"><span data-stu-id="e940c-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="e940c-138">Zjednodušuje [testování částí](../testing-and-debugging/unit-testing-controllers-in-web-api.md) vašich řadičů.</span><span class="sxs-lookup"><span data-stu-id="e940c-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="e940c-139">Přesune společnou logiku pro vytváření odpovědí HTTP na samostatné třídy.</span><span class="sxs-lookup"><span data-stu-id="e940c-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="e940c-140">Provede záměr akce kontroleru tím, že skryje podrobnosti nízké úrovně konstrukce odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e940c-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="e940c-141">**IHttpActionResult** obsahuje jedinou metodu **metody ExecuteAsync**, která asynchronně vytvoří instanci **HttpResponseMessage** .</span><span class="sxs-lookup"><span data-stu-id="e940c-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="e940c-142">Pokud akce kontroleru vrátí **IHttpActionResult**, webové rozhraní API zavolá metodu **metody ExecuteAsync** , která vytvoří **HttpResponseMessage**.</span><span class="sxs-lookup"><span data-stu-id="e940c-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="e940c-143">Pak převede **HttpResponseMessage** na zprávu odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="e940c-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="e940c-144">Tady je jednoduchá implementace **IHttpActionResult** , která vytvoří odpověď v podobě prostého textu:</span><span class="sxs-lookup"><span data-stu-id="e940c-144">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="e940c-145">Příklad akce kontroleru:</span><span class="sxs-lookup"><span data-stu-id="e940c-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="e940c-146">Základě</span><span class="sxs-lookup"><span data-stu-id="e940c-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="e940c-147">Častěji používáte implementace **IHttpActionResult** definované v oboru názvů **[System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="e940c-147">More often, you use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="e940c-148">Třída **ApiController** definuje pomocné metody, které vracejí tyto předdefinované výsledky akcí.</span><span class="sxs-lookup"><span data-stu-id="e940c-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="e940c-149">Pokud se v následujícím příkladu požadavek neshoduje s existujícím ID produktu, kontroler zavolá [ApiController. NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) , aby vytvořil odpověď 404 (Nenalezeno).</span><span class="sxs-lookup"><span data-stu-id="e940c-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="e940c-150">V opačném případě kontroler zavolá [ApiController. ok](https://msdn.microsoft.com/library/dn314591.aspx), čímž se vytvoří odpověď 200 (ok), která obsahuje daný produkt.</span><span class="sxs-lookup"><span data-stu-id="e940c-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="e940c-151">Jiné návratové typy</span><span class="sxs-lookup"><span data-stu-id="e940c-151">Other Return Types</span></span>

<span data-ttu-id="e940c-152">Pro všechny ostatní návratové typy používá webové rozhraní API [formátovací modul médií](../formats-and-model-binding/media-formatters.md) k serializaci návratové hodnoty.</span><span class="sxs-lookup"><span data-stu-id="e940c-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="e940c-153">Webové rozhraní API zapisuje serializovanou hodnotu do těla odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e940c-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="e940c-154">Stavový kód odpovědi je 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="e940c-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="e940c-155">Nevýhodou tohoto přístupu je, že nemůžete přímo vracet kód chyby, například 404.</span><span class="sxs-lookup"><span data-stu-id="e940c-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="e940c-156">Můžete však vyvolat **HttpResponseException** pro kódy chyb.</span><span class="sxs-lookup"><span data-stu-id="e940c-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="e940c-157">Další informace najdete v tématu [zpracování výjimek ve webovém rozhraní API ASP.NET](../error-handling/exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="e940c-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="e940c-158">Webové rozhraní API používá k výběru formátovacího modulu hlavičku Accept v žádosti.</span><span class="sxs-lookup"><span data-stu-id="e940c-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="e940c-159">Další informace najdete v tématu [vyjednávání obsahu](../formats-and-model-binding/content-negotiation.md).</span><span class="sxs-lookup"><span data-stu-id="e940c-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="e940c-160">Příklad žádosti</span><span class="sxs-lookup"><span data-stu-id="e940c-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="e940c-161">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="e940c-161">Example response</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
