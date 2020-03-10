---
uid: web-api/overview/error-handling/exception-handling
title: Zpracování výjimek ve webovém rozhraní API ASP.NET – ASP.NET 4. x
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622316"
---
# <a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="813f8-102">Zpracování výjimek ve webovém rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="813f8-102">Exception Handling in ASP.NET Web API</span></span>

<span data-ttu-id="813f8-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="813f8-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="813f8-104">Tento článek popisuje zpracování chyb a výjimek v ASP.NET webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="813f8-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="813f8-105">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="813f8-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="813f8-106">Filtry výjimek</span><span class="sxs-lookup"><span data-stu-id="813f8-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="813f8-107">Registrace filtrů výjimek</span><span class="sxs-lookup"><span data-stu-id="813f8-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="813f8-108">HttpError</span><span class="sxs-lookup"><span data-stu-id="813f8-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="813f8-109">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="813f8-109">HttpResponseException</span></span>

<span data-ttu-id="813f8-110">Co se stane, když kontroler webového rozhraní API vyvolá nezachycenou výjimku?</span><span class="sxs-lookup"><span data-stu-id="813f8-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="813f8-111">Ve výchozím nastavení se většina výjimek převede na odpověď HTTP se stavovým kódem 500, interní chyba serveru.</span><span class="sxs-lookup"><span data-stu-id="813f8-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="813f8-112">Typ **HttpResponseException** je zvláštní případ.</span><span class="sxs-lookup"><span data-stu-id="813f8-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="813f8-113">Tato výjimka vrátí jakýkoli stavový kód HTTP, který zadáte v konstruktoru výjimky.</span><span class="sxs-lookup"><span data-stu-id="813f8-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="813f8-114">Například následující metoda vrátí 404, nebyla nalezena, pokud parametr *ID* není platný.</span><span class="sxs-lookup"><span data-stu-id="813f8-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="813f8-115">Pro lepší kontrolu nad odpovědí můžete také sestavit celou zprávu odpovědi a zahrnout ji do **HttpResponseException:**</span><span class="sxs-lookup"><span data-stu-id="813f8-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="813f8-116">Filtry výjimek</span><span class="sxs-lookup"><span data-stu-id="813f8-116">Exception Filters</span></span>

<span data-ttu-id="813f8-117">Můžete přizpůsobit, jak webové rozhraní API zpracovává výjimky pomocí zápisu *filtru výjimek*.</span><span class="sxs-lookup"><span data-stu-id="813f8-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="813f8-118">Filtr výjimek je proveden, pokud metoda kontroleru vyvolá jakoukoli neošetřenou výjimku, *která není* **HttpResponseException** výjimkou.</span><span class="sxs-lookup"><span data-stu-id="813f8-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="813f8-119">Typ **HttpResponseException** je zvláštní případ, protože je navržený speciálně pro vracení odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="813f8-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="813f8-120">Filtry výjimek implementují rozhraní **System. Web. http. filters. IExceptionFilter** .</span><span class="sxs-lookup"><span data-stu-id="813f8-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="813f8-121">Nejjednodušší způsob, jak napsat filtr výjimky, je odvozovat z třídy **System. Web. http. filters. ExceptionFilterAttribute** a přepsat metodu **s výjimkou** .</span><span class="sxs-lookup"><span data-stu-id="813f8-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="813f8-122">Filtry výjimek ve webovém rozhraní API ASP.NET jsou podobné těm v ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="813f8-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="813f8-123">Jsou však deklarovány v samostatném oboru názvů a funkci samostatně.</span><span class="sxs-lookup"><span data-stu-id="813f8-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="813f8-124">Konkrétně třída **HandleErrorAttribute** používaná v MVC nezpracovává výjimky vyvolané řadiči webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="813f8-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>

<span data-ttu-id="813f8-125">Tady je filtr, který převede výjimky **NotImplementedException** na stavový kód http 501, není implementováno:</span><span class="sxs-lookup"><span data-stu-id="813f8-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="813f8-126">Vlastnost **Response** objektu **HttpActionExecutedContext** obsahuje zprávu odpovědi HTTP, která se pošle klientovi.</span><span class="sxs-lookup"><span data-stu-id="813f8-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="813f8-127">Registrace filtrů výjimek</span><span class="sxs-lookup"><span data-stu-id="813f8-127">Registering Exception Filters</span></span>

<span data-ttu-id="813f8-128">Existuje několik způsobů, jak zaregistrovat filtr výjimky webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="813f8-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="813f8-129">Podle akce</span><span class="sxs-lookup"><span data-stu-id="813f8-129">By action</span></span>
- <span data-ttu-id="813f8-130">Podle kontroléru</span><span class="sxs-lookup"><span data-stu-id="813f8-130">By controller</span></span>
- <span data-ttu-id="813f8-131">univerzál</span><span class="sxs-lookup"><span data-stu-id="813f8-131">Globally</span></span>

<span data-ttu-id="813f8-132">Chcete-li použít filtr na konkrétní akci, přidejte filtr jako atribut do akce:</span><span class="sxs-lookup"><span data-stu-id="813f8-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="813f8-133">Chcete-li použít filtr na všechny akce na řadiči, přidejte filtr jako atribut do třídy Controller:</span><span class="sxs-lookup"><span data-stu-id="813f8-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="813f8-134">Pokud chcete filtr použít globálně na všechny řadiče webového rozhraní API, přidejte instanci filtru do kolekce **GlobalConfiguration. Configuration. filters** .</span><span class="sxs-lookup"><span data-stu-id="813f8-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="813f8-135">Filtry výjimek v této kolekci platí pro všechny akce kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="813f8-135">Exception filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="813f8-136">Pokud k vytvoření projektu použijete šablonu projektu webová aplikace ASP.NET MVC 4, vložte svůj konfigurační kód webového rozhraní API do třídy `WebApiConfig`, která je umístěna ve složce App\_Start:</span><span class="sxs-lookup"><span data-stu-id="813f8-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="813f8-137">HttpError</span><span class="sxs-lookup"><span data-stu-id="813f8-137">HttpError</span></span>

<span data-ttu-id="813f8-138">Objekt **HttpError** poskytuje konzistentní způsob, jak vracet informace o chybě v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="813f8-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="813f8-139">Následující příklad ukazuje, jak vrátit stavový kód HTTP 404 (Nenalezeno) s **HttpError** v těle odpovědi.</span><span class="sxs-lookup"><span data-stu-id="813f8-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="813f8-140">**CreateErrorResponse** je metoda rozšíření definovaná v třídě **System .NET. http. HttpRequestMessageExtensions** .</span><span class="sxs-lookup"><span data-stu-id="813f8-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="813f8-141">Interně **CreateErrorResponse** vytvoří instanci **HttpError** a pak vytvoří **HttpResponseMessage** obsahující **HttpError**.</span><span class="sxs-lookup"><span data-stu-id="813f8-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="813f8-142">V tomto příkladu, pokud je metoda úspěšná, vrátí produkt v odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="813f8-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="813f8-143">Pokud se ale požadovaný produkt nenajde, odpověď HTTP obsahuje **HttpError** v textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="813f8-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="813f8-144">Odpověď může vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="813f8-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="813f8-145">Všimněte si, že v tomto příkladu byl v tomto příkladu serializován **HttpError** do formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="813f8-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="813f8-146">Jednou z výhod použití **HttpError** je to, že projde stejným procesem [pro vyjednávání obsahu](../formats-and-model-binding/content-negotiation.md) a serializaci jako jakýkoli jiný model silného typu.</span><span class="sxs-lookup"><span data-stu-id="813f8-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="813f8-147">HttpError a ověření modelu</span><span class="sxs-lookup"><span data-stu-id="813f8-147">HttpError and Model Validation</span></span>

<span data-ttu-id="813f8-148">Pro ověření modelu můžete předat stav modelu do **CreateErrorResponse**, aby se zahrnuly chyby ověřování v odpovědi:</span><span class="sxs-lookup"><span data-stu-id="813f8-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="813f8-149">Tento příklad může vracet následující odpověď:</span><span class="sxs-lookup"><span data-stu-id="813f8-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="813f8-150">Další informace o ověřování modelu najdete v tématu [ověřování modelu v ASP.NET webovém rozhraní API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="813f8-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="813f8-151">Použití HttpError s HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="813f8-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="813f8-152">Předchozí příklady vrátí zprávu **HttpResponseMessage** z akce kontroleru, ale můžete také použít **HttpResponseException** a vrátit **HttpError**.</span><span class="sxs-lookup"><span data-stu-id="813f8-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="813f8-153">To vám umožní vracet model silného typu v normálním případě úspěchu a pořád vracet **HttpError** , pokud dojde k chybě:</span><span class="sxs-lookup"><span data-stu-id="813f8-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
