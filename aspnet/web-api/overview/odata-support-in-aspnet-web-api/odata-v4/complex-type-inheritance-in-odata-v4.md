---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Dědičnost komplexního typu v OData V4 s webovým rozhraním API ASP.NET | Microsoft Docs
author: microsoft
description: Podle specifikace OData v4 může komplexní typ dědit z jiného komplexního typu. (Komplexní typ je strukturovaný typ bez klíče.) Webové rozhraní API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556306"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="7d15e-104">Dědičnost komplexního typu v OData V4 s webovým rozhraním API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7d15e-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="7d15e-105">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7d15e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7d15e-106">Podle [specifikace](http://www.odata.org/documentation/odata-version-4-0/)OData v4 může komplexní typ dědit z jiného komplexního typu.</span><span class="sxs-lookup"><span data-stu-id="7d15e-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="7d15e-107">( *Komplexní* typ je strukturovaný typ bez klíče.) Webové rozhraní API OData 5,3 podporuje dědičnost komplexního typu.</span><span class="sxs-lookup"><span data-stu-id="7d15e-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="7d15e-108">V tomto tématu se dozvíte, jak vytvořit entity data model (EDM) se složitými typy dědičnosti.</span><span class="sxs-lookup"><span data-stu-id="7d15e-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="7d15e-109">Úplný zdrojový kód naleznete v tématu [Ukázka dědičnosti komplexního typu OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span><span class="sxs-lookup"><span data-stu-id="7d15e-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7d15e-110">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="7d15e-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7d15e-111">Webové rozhraní API OData 5,3</span><span class="sxs-lookup"><span data-stu-id="7d15e-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="7d15e-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="7d15e-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="7d15e-113">Hierarchie modelů</span><span class="sxs-lookup"><span data-stu-id="7d15e-113">Model Hierarchy</span></span>

<span data-ttu-id="7d15e-114">K ilustraci dědičnosti komplexního typu používáme následující hierarchii tříd.</span><span class="sxs-lookup"><span data-stu-id="7d15e-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="7d15e-115">`Shape` je abstraktní komplexní typ.</span><span class="sxs-lookup"><span data-stu-id="7d15e-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="7d15e-116">`Rectangle`, `Triangle`a `Circle` jsou komplexní typy odvozené od `Shape`a `RoundRectangle` jsou odvozeny z `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="7d15e-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="7d15e-117">`Window` je typ entity a obsahuje instanci `Shape`.</span><span class="sxs-lookup"><span data-stu-id="7d15e-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="7d15e-118">Zde jsou třídy CLR, které definují tyto typy.</span><span class="sxs-lookup"><span data-stu-id="7d15e-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="7d15e-119">Sestavení modelu EDM</span><span class="sxs-lookup"><span data-stu-id="7d15e-119">Build the EDM Model</span></span>

<span data-ttu-id="7d15e-120">Chcete-li vytvořit EDM, můžete použít **ODataConventionModelBuilder**, který odvodí vztahy dědičnosti z typů CLR.</span><span class="sxs-lookup"><span data-stu-id="7d15e-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="7d15e-121">Můžete také vytvořit EDM explicitně pomocí **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="7d15e-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="7d15e-122">Tím se získá více kódu, ale získáte větší kontrolu nad modelem EDM.</span><span class="sxs-lookup"><span data-stu-id="7d15e-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="7d15e-123">Tyto dva příklady vytvoří stejné schéma EDM.</span><span class="sxs-lookup"><span data-stu-id="7d15e-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="7d15e-124">Dokument metadat</span><span class="sxs-lookup"><span data-stu-id="7d15e-124">Metadata Document</span></span>

<span data-ttu-id="7d15e-125">Tady je dokument metadat OData, který ukazuje dědičnost komplexního typu.</span><span class="sxs-lookup"><span data-stu-id="7d15e-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="7d15e-126">V dokumentu metadat vidíte, že:</span><span class="sxs-lookup"><span data-stu-id="7d15e-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="7d15e-127">`Shape` komplexní typ je abstraktní.</span><span class="sxs-lookup"><span data-stu-id="7d15e-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="7d15e-128">Komplexní typ `Rectangle`, `Triangle`a `Circle` mají základní typ `Shape`.</span><span class="sxs-lookup"><span data-stu-id="7d15e-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="7d15e-129">Typ `RoundRectangle` má `Rectangle`základního typu.</span><span class="sxs-lookup"><span data-stu-id="7d15e-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="7d15e-130">Přetypování složitých typů</span><span class="sxs-lookup"><span data-stu-id="7d15e-130">Casting Complex Types</span></span>

<span data-ttu-id="7d15e-131">Přetypování na komplexní typy se teď podporuje.</span><span class="sxs-lookup"><span data-stu-id="7d15e-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="7d15e-132">Například následující dotaz přetypování `Shape` na `Rectangle`.</span><span class="sxs-lookup"><span data-stu-id="7d15e-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="7d15e-133">Zde je datová část odpovědi:</span><span class="sxs-lookup"><span data-stu-id="7d15e-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
