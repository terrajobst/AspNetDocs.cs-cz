---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: Ověřování modelu v ASP.NET Web API – ASP.NET 4. x
author: MikeWasson
description: Přehled ověřování modelu ve webovém rozhraní API ASP.NET pro ASP.NET 4. x
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557237"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="2e120-103">Ověření modelu ve webovém rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2e120-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="2e120-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2e120-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2e120-105">Tento článek ukazuje, jak přidávat poznámky k vašim modelům, používat poznámky k ověřování dat a zpracovávat chyby ověřování ve webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2e120-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="2e120-106">Když klient odešle data do webového rozhraní API, často chcete ověřit data před jakýmkoli zpracováním.</span><span class="sxs-lookup"><span data-stu-id="2e120-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="2e120-107">Datové poznámky</span><span class="sxs-lookup"><span data-stu-id="2e120-107">Data Annotations</span></span>

<span data-ttu-id="2e120-108">Ve webovém rozhraní API ASP.NET můžete použít atributy z oboru názvů [System. ComponentModel. DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) k nastavení ověřovacích pravidel pro vlastnosti v modelu.</span><span class="sxs-lookup"><span data-stu-id="2e120-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="2e120-109">Vezměte v úvahu následující model:</span><span class="sxs-lookup"><span data-stu-id="2e120-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="2e120-110">Pokud jste v ASP.NET MVC použili ověřování modelu, mělo by to vypadat dobře.</span><span class="sxs-lookup"><span data-stu-id="2e120-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="2e120-111">**Požadovaný** atribut říká, že vlastnost `Name` nesmí mít hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="2e120-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="2e120-112">Atribut **Range** uvádí, že `Weight` musí být mezi nulou a 999.</span><span class="sxs-lookup"><span data-stu-id="2e120-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="2e120-113">Předpokládejme, že klient pošle požadavek POST s následující reprezentací JSON:</span><span class="sxs-lookup"><span data-stu-id="2e120-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="2e120-114">Můžete vidět, že klient neobsahuje vlastnost `Name`, která je označena jako povinná.</span><span class="sxs-lookup"><span data-stu-id="2e120-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="2e120-115">Když webové rozhraní API převede JSON na instanci `Product`, ověří `Product` na základě ověřovacích atributů.</span><span class="sxs-lookup"><span data-stu-id="2e120-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="2e120-116">V akci kontroleru si můžete ověřit, jestli je model platný:</span><span class="sxs-lookup"><span data-stu-id="2e120-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="2e120-117">Ověřování modelu nezaručuje, že jsou data klienta bezpečná.</span><span class="sxs-lookup"><span data-stu-id="2e120-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="2e120-118">Další ověřování může být potřeba v jiných vrstvách aplikace.</span><span class="sxs-lookup"><span data-stu-id="2e120-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="2e120-119">(Například datová vrstva může vynutit omezení cizího klíče.) Tento kurz [s použitím webového rozhraní API Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) prozkoumává některé z těchto problémů.</span><span class="sxs-lookup"><span data-stu-id="2e120-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="2e120-120">Pokud klient opustí některé vlastnosti, stane se pod položkou " **odesílání"** .</span><span class="sxs-lookup"><span data-stu-id="2e120-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="2e120-121">Předpokládejme například, že klient odesílá následující:</span><span class="sxs-lookup"><span data-stu-id="2e120-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="2e120-122">V tomto případě klient neurčil hodnoty pro `Price` ani `Weight`.</span><span class="sxs-lookup"><span data-stu-id="2e120-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="2e120-123">Formátovací modul JSON přiřadí výchozí hodnotu nula chybějícím vlastnostem.</span><span class="sxs-lookup"><span data-stu-id="2e120-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="2e120-124">Stav modelu je platný, protože nula je platná hodnota pro tyto vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="2e120-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="2e120-125">Bez ohledu na to, jestli se jedná o problém, závisí na vašem scénáři.</span><span class="sxs-lookup"><span data-stu-id="2e120-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="2e120-126">Například v operaci aktualizace můžete chtít rozlišovat mezi "0" a "nenastavenou".</span><span class="sxs-lookup"><span data-stu-id="2e120-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="2e120-127">Chcete-li vynutit, aby klienti nastavili hodnotu, nastavte vlastnost na hodnotu null a nastavte **požadovaný** atribut:</span><span class="sxs-lookup"><span data-stu-id="2e120-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="2e120-128">**"** Při přeposílání": klient může také odesílat *více* dat, než jste očekávali.</span><span class="sxs-lookup"><span data-stu-id="2e120-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="2e120-129">Příklad:</span><span class="sxs-lookup"><span data-stu-id="2e120-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="2e120-130">V tomto příkladu obsahuje JSON vlastnost ("Color"), která neexistuje v modelu `Product`.</span><span class="sxs-lookup"><span data-stu-id="2e120-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="2e120-131">V tomto případě formátovací modul JSON jednoduše tuto hodnotu ignoruje.</span><span class="sxs-lookup"><span data-stu-id="2e120-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="2e120-132">(Formátovací modul XML je stejný.) Při převzetí služeb při selhání dochází k problémům, pokud má váš model vlastnosti, které máte v úmyslu jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="2e120-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="2e120-133">Příklad:</span><span class="sxs-lookup"><span data-stu-id="2e120-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="2e120-134">Nechcete, aby uživatelé aktualizovali vlastnost `IsAdmin` a mohli se zvýšit oprávnění správcům!</span><span class="sxs-lookup"><span data-stu-id="2e120-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="2e120-135">Nejbezpečnější strategií je použít třídu modelu, která přesně odpovídá, co může klient odesílat:</span><span class="sxs-lookup"><span data-stu-id="2e120-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="2e120-136">Wilson Blogový příspěvek "[ověření vstupu vs. ověřování modelů v ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" obsahuje dobrou diskuzi o tom, jak se účtují a proúčtují.</span><span class="sxs-lookup"><span data-stu-id="2e120-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="2e120-137">I když je příspěvek o ASP.NET MVC 2, problémy jsou stále relevantní pro webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2e120-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>

## <a name="handling-validation-errors"></a><span data-ttu-id="2e120-138">Zpracování chyb ověřování</span><span class="sxs-lookup"><span data-stu-id="2e120-138">Handling Validation Errors</span></span>

<span data-ttu-id="2e120-139">Webové rozhraní API nevrátí klientovi automaticky chybu, pokud se ověření nepovede.</span><span class="sxs-lookup"><span data-stu-id="2e120-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="2e120-140">Je až do akce kontroleru ke kontrole stavu modelu a odpovídajícím způsobem reagovat.</span><span class="sxs-lookup"><span data-stu-id="2e120-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="2e120-141">Můžete také vytvořit filtr akcí pro kontrolu stavu modelu před vyvoláním akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="2e120-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="2e120-142">Příklad ukazuje následující kód:</span><span class="sxs-lookup"><span data-stu-id="2e120-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="2e120-143">Pokud ověření modelu neproběhne úspěšně, vrátí tento filtr odpověď HTTP, která obsahuje chyby ověřování.</span><span class="sxs-lookup"><span data-stu-id="2e120-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="2e120-144">V takovém případě není vyvolána akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="2e120-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="2e120-145">Pokud chcete tento filtr použít u všech řadičů webového rozhraní API, přidejte do kolekce **HttpConfiguration. filters** během konfigurace instanci filtru:</span><span class="sxs-lookup"><span data-stu-id="2e120-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="2e120-146">Další možností je nastavit filtr jako atribut na jednotlivé řadiče nebo akce kontroleru:</span><span class="sxs-lookup"><span data-stu-id="2e120-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
