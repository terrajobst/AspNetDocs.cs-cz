---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Komplexní dědičnost typů v OData v4 s rozhraním ASP.NET Web API | Dokumentace Microsoftu
author: microsoft
description: Podle specifikace v4 pracovní verze protokolu OData komplexní typ může dědit z jiného komplexního typu. (Komplexní typ je strukturovaného typu bez klíče.) Webové rozhraní API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132746"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="caa71-104">Komplexní dědičnost typů v OData v4 s rozhraním ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="caa71-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="caa71-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="caa71-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="caa71-106">Podle OData v4 [specifikace](http://www.odata.org/documentation/odata-version-4-0/), komplexní typ může dědit z jiného komplexního typu.</span><span class="sxs-lookup"><span data-stu-id="caa71-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="caa71-107">(A *komplexní* typ je typ structured bez klíče.) Web API OData 5.3 podporuje komplexní dědičnost typů.</span><span class="sxs-lookup"><span data-stu-id="caa71-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="caa71-108">Toto téma ukazuje, jak vytvářet entity data model (EDM) s komplexní dědičnost typů.</span><span class="sxs-lookup"><span data-stu-id="caa71-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="caa71-109">Úplný zdrojový kód, naleznete v tématu [OData komplexní typ dědičnosti ukázka](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span><span class="sxs-lookup"><span data-stu-id="caa71-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="caa71-110">V tomto kurzu použili verze softwaru</span><span class="sxs-lookup"><span data-stu-id="caa71-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="caa71-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="caa71-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="caa71-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="caa71-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="caa71-113">Hierarchie modelu</span><span class="sxs-lookup"><span data-stu-id="caa71-113">Model Hierarchy</span></span>

<span data-ttu-id="caa71-114">Pro ilustraci komplexní dědičnost typů, používáme následující hierarchie tříd.</span><span class="sxs-lookup"><span data-stu-id="caa71-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="caa71-115">`Shape` je abstraktní komplexního typu.</span><span class="sxs-lookup"><span data-stu-id="caa71-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="caa71-116">`Rectangle`, `Triangle`, a `Circle` jsou komplexní typy odvozené z `Shape`, a `RoundRectangle` je odvozena z `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="caa71-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="caa71-117">`Window` je typ entity a obsahuje `Shape` instance.</span><span class="sxs-lookup"><span data-stu-id="caa71-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="caa71-118">Tady jsou třídy CLR, které definují tyto typy.</span><span class="sxs-lookup"><span data-stu-id="caa71-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="caa71-119">Sestavení modelu EDM</span><span class="sxs-lookup"><span data-stu-id="caa71-119">Build the EDM Model</span></span>

<span data-ttu-id="caa71-120">Chcete-li vytvořit EDM, můžete použít **ODataConventionModelBuilder**, která odvodí vztahy dědičnosti z typů CLR.</span><span class="sxs-lookup"><span data-stu-id="caa71-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="caa71-121">Můžete také sestavit EDM explicitně, pomocí **Tvůrce ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="caa71-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="caa71-122">To trvá více kódu, ale dává větší kontrolu nad modelu EDM.</span><span class="sxs-lookup"><span data-stu-id="caa71-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="caa71-123">Tyto dva příklady vytvoření stejné schéma modelu EDM.</span><span class="sxs-lookup"><span data-stu-id="caa71-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="caa71-124">Dokument metadat</span><span class="sxs-lookup"><span data-stu-id="caa71-124">Metadata Document</span></span>

<span data-ttu-id="caa71-125">Tady je dokument metadat OData, zobrazuje komplexní dědičnost typů.</span><span class="sxs-lookup"><span data-stu-id="caa71-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="caa71-126">Dokument metadat uvidíte, které:</span><span class="sxs-lookup"><span data-stu-id="caa71-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="caa71-127">`Shape` Komplexní typ je abstraktní.</span><span class="sxs-lookup"><span data-stu-id="caa71-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="caa71-128">`Rectangle`, `Triangle`, A `Circle` komplexního typu mít základní typ `Shape`.</span><span class="sxs-lookup"><span data-stu-id="caa71-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="caa71-129">`RoundRectangle` Typ má základní typ `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="caa71-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="caa71-130">Přetypování komplexní typy</span><span class="sxs-lookup"><span data-stu-id="caa71-130">Casting Complex Types</span></span>

<span data-ttu-id="caa71-131">Přetypování na komplexní typy se teď podporuje.</span><span class="sxs-lookup"><span data-stu-id="caa71-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="caa71-132">Například následující dotaz přetypování `Shape` k `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="caa71-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="caa71-133">Tady je datové části odpovědi:</span><span class="sxs-lookup"><span data-stu-id="caa71-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
