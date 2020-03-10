---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Otevřené typy v OData V4 s webovým rozhraním API ASP.NET | Microsoft Docs
author: microsoft
description: V OData v4 je otevřený typ strukturovaný typ, který obsahuje dynamické vlastnosti, kromě jakýchkoli vlastností, které jsou deklarovány v definici typu. Otevřít...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622176"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="91bc3-104">Otevřené typy v OData V4 s webovým rozhraním API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="91bc3-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="91bc3-105">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="91bc3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="91bc3-106">V OData v4 je *otevřený typ* strukturovaný typ, který obsahuje dynamické vlastnosti, kromě jakýchkoli vlastností, které jsou deklarovány v definici typu.</span><span class="sxs-lookup"><span data-stu-id="91bc3-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="91bc3-107">Otevřené typy umožňují přidat flexibilitu pro vaše datové modely.</span><span class="sxs-lookup"><span data-stu-id="91bc3-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="91bc3-108">V tomto kurzu se dozvíte, jak používat otevřené typy v ASP.NET webového rozhraní API OData.</span><span class="sxs-lookup"><span data-stu-id="91bc3-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="91bc3-109">V tomto kurzu se předpokládá, že už víte, jak ve webovém rozhraní API ASP.NET vytvořit koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="91bc3-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="91bc3-110">Pokud ne, začněte načtením a nejprve [vytvořte koncový bod OData v4](create-an-odata-v4-endpoint.md) .</span><span class="sxs-lookup"><span data-stu-id="91bc3-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="91bc3-111">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="91bc3-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="91bc3-112">Webové rozhraní API OData 5,3</span><span class="sxs-lookup"><span data-stu-id="91bc3-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="91bc3-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="91bc3-113">OData v4</span></span>

<span data-ttu-id="91bc3-114">Nejdřív některé terminologie OData:</span><span class="sxs-lookup"><span data-stu-id="91bc3-114">First, some OData terminology:</span></span>

- <span data-ttu-id="91bc3-115">Typ entity: strukturovaný typ s klíčem.</span><span class="sxs-lookup"><span data-stu-id="91bc3-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="91bc3-116">Komplexní typ: strukturovaný typ bez klíče.</span><span class="sxs-lookup"><span data-stu-id="91bc3-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="91bc3-117">Typ otevřeného typu: typ s dynamickými vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="91bc3-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="91bc3-118">Je možné otevřít oba typy entit a komplexní typy.</span><span class="sxs-lookup"><span data-stu-id="91bc3-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="91bc3-119">Hodnotou dynamické vlastnosti může být primitivní typ, komplexní typ nebo Výčtový typ. nebo kolekci některého z těchto typů.</span><span class="sxs-lookup"><span data-stu-id="91bc3-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="91bc3-120">Další informace o otevřených typech najdete v tématu [specifikace OData v4](http://www.odata.org/documentation/odata-version-4-0/).</span><span class="sxs-lookup"><span data-stu-id="91bc3-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="91bc3-121">Instalace webových knihoven OData</span><span class="sxs-lookup"><span data-stu-id="91bc3-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="91bc3-122">Pomocí Správce balíčků NuGet nainstalujte nejnovější knihovny Web API OData.</span><span class="sxs-lookup"><span data-stu-id="91bc3-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="91bc3-123">V okně konzoly Správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="91bc3-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="91bc3-124">Definování typů CLR</span><span class="sxs-lookup"><span data-stu-id="91bc3-124">Define the CLR Types</span></span>

<span data-ttu-id="91bc3-125">Začněte tím, že definujete modely EDM jako typy CLR.</span><span class="sxs-lookup"><span data-stu-id="91bc3-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="91bc3-126">Při vytvoření model EDM (Entity Data Model) (EDM),</span><span class="sxs-lookup"><span data-stu-id="91bc3-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="91bc3-127">`Category` je typ výčtu.</span><span class="sxs-lookup"><span data-stu-id="91bc3-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="91bc3-128">`Address` je komplexní typ.</span><span class="sxs-lookup"><span data-stu-id="91bc3-128">`Address` is a complex type.</span></span> <span data-ttu-id="91bc3-129">(Nemá klíč, takže se nejedná o typ entity.)</span><span class="sxs-lookup"><span data-stu-id="91bc3-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="91bc3-130">`Customer` je typ entity.</span><span class="sxs-lookup"><span data-stu-id="91bc3-130">`Customer` is an entity type.</span></span> <span data-ttu-id="91bc3-131">(Obsahuje klíč.)</span><span class="sxs-lookup"><span data-stu-id="91bc3-131">(It has a key.)</span></span>
- <span data-ttu-id="91bc3-132">`Press` je otevřený komplexní typ.</span><span class="sxs-lookup"><span data-stu-id="91bc3-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="91bc3-133">`Book` je otevřený typ entity.</span><span class="sxs-lookup"><span data-stu-id="91bc3-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="91bc3-134">Chcete-li vytvořit otevřený typ, musí mít typ CLR vlastnost typu `IDictionary<string, object>`, která obsahuje dynamické vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="91bc3-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="91bc3-135">Sestavení modelu EDM</span><span class="sxs-lookup"><span data-stu-id="91bc3-135">Build the EDM Model</span></span>

<span data-ttu-id="91bc3-136">Použijete-li **ODataConventionModelBuilder** k vytvoření EDM, `Press` a `Book` jsou automaticky přidány jako otevřené typy, a to na základě přítomnosti vlastnosti `IDictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="91bc3-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="91bc3-137">Můžete také vytvořit EDM explicitně pomocí **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="91bc3-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="91bc3-138">Přidat kontroler OData</span><span class="sxs-lookup"><span data-stu-id="91bc3-138">Add an OData Controller</span></span>

<span data-ttu-id="91bc3-139">Dále přidejte kontroler OData.</span><span class="sxs-lookup"><span data-stu-id="91bc3-139">Next, add an OData controller.</span></span> <span data-ttu-id="91bc3-140">Pro účely tohoto kurzu budeme používat zjednodušený kontroler, který podporuje jenom požadavky GET a POST a používá seznam v paměti k ukládání entit.</span><span class="sxs-lookup"><span data-stu-id="91bc3-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="91bc3-141">Všimněte si, že první instance `Book` nemá žádné dynamické vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="91bc3-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="91bc3-142">Druhá instance `Book` má následující dynamické vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="91bc3-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="91bc3-143">"Publikováno": primitivní typ</span><span class="sxs-lookup"><span data-stu-id="91bc3-143">"Published": Primitive type</span></span>
- <span data-ttu-id="91bc3-144">"Autoři": kolekce primitivních typů</span><span class="sxs-lookup"><span data-stu-id="91bc3-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="91bc3-145">"OtherCategories": kolekce typů výčtu.</span><span class="sxs-lookup"><span data-stu-id="91bc3-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="91bc3-146">Vlastnost `Press` této instance `Book` má také následující dynamické vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="91bc3-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="91bc3-147">"Blog": primitivní typ</span><span class="sxs-lookup"><span data-stu-id="91bc3-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="91bc3-148">"Adresa": komplexní typ</span><span class="sxs-lookup"><span data-stu-id="91bc3-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="91bc3-149">Dotazování na metadata</span><span class="sxs-lookup"><span data-stu-id="91bc3-149">Query the Metadata</span></span>

<span data-ttu-id="91bc3-150">K získání dokumentu metadat OData odešlete požadavek GET na `~/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="91bc3-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="91bc3-151">Text odpovědi by měl vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="91bc3-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="91bc3-152">V dokumentu metadat vidíte, že:</span><span class="sxs-lookup"><span data-stu-id="91bc3-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="91bc3-153">U typů `Book` a `Press` je hodnota atributu `OpenType` true.</span><span class="sxs-lookup"><span data-stu-id="91bc3-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="91bc3-154">Typy `Customer` a `Address` nemají tento atribut.</span><span class="sxs-lookup"><span data-stu-id="91bc3-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="91bc3-155">Typ entity `Book` obsahuje tři deklarované vlastnosti: ISBN, title a Press.</span><span class="sxs-lookup"><span data-stu-id="91bc3-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="91bc3-156">Metadata OData neobsahují vlastnost `Book.Properties` z třídy CLR.</span><span class="sxs-lookup"><span data-stu-id="91bc3-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="91bc3-157">Podobně `Press` komplexní typ obsahuje pouze dvě deklarované vlastnosti: název a kategorie.</span><span class="sxs-lookup"><span data-stu-id="91bc3-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="91bc3-158">Metadata neobsahují vlastnost `Press.DynamicProperties` z třídy CLR.</span><span class="sxs-lookup"><span data-stu-id="91bc3-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="91bc3-159">Dotazování entity</span><span class="sxs-lookup"><span data-stu-id="91bc3-159">Query an Entity</span></span>

<span data-ttu-id="91bc3-160">Pokud chcete získat knihu se symbolem ISBN rovnající se "978-0-7356-7942-9", odešlete požadavek GET na `~/Books('978-0-7356-7942-9')`.</span><span class="sxs-lookup"><span data-stu-id="91bc3-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="91bc3-161">Tělo odpovědi by mělo vypadat podobně jako následující.</span><span class="sxs-lookup"><span data-stu-id="91bc3-161">The response body should look similar to the following.</span></span> <span data-ttu-id="91bc3-162">(Odsazené tak, aby se čitelnější.)</span><span class="sxs-lookup"><span data-stu-id="91bc3-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="91bc3-163">Všimněte si, že dynamické vlastnosti jsou zahrnuty jako vložené s deklarovanými vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="91bc3-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="91bc3-164">PUBLIKOVÁNÍ entity</span><span class="sxs-lookup"><span data-stu-id="91bc3-164">POST an Entity</span></span>

<span data-ttu-id="91bc3-165">Chcete-li přidat entitu knihy, odešlete požadavek POST na `~/Books`.</span><span class="sxs-lookup"><span data-stu-id="91bc3-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="91bc3-166">Klient může v datové části požadavku nastavit dynamické vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="91bc3-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="91bc3-167">Tady je příklad žádosti.</span><span class="sxs-lookup"><span data-stu-id="91bc3-167">Here is an example request.</span></span> <span data-ttu-id="91bc3-168">Poznamenejte si vlastnosti Price a Publikováno.</span><span class="sxs-lookup"><span data-stu-id="91bc3-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="91bc3-169">Pokud nastavíte zarážku v metodě kontroleru, vidíte, že webové rozhraní API přidalo tyto vlastnosti do slovníku `Properties`.</span><span class="sxs-lookup"><span data-stu-id="91bc3-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="91bc3-170">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="91bc3-170">Additional Resources</span></span>

[<span data-ttu-id="91bc3-171">Ukázka otevřeného typu OData</span><span class="sxs-lookup"><span data-stu-id="91bc3-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
