---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Vytvoření typu Singleton v OData v4 pomocí webového rozhraní API 2,2 | Microsoft Docs
author: rick-anderson
description: V tomto tématu se dozvíte, jak definovat typ singleton v koncovém bodu OData ve webovém rozhraní API 2,2.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622085"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="3688b-103">Vytvoření typu Singleton v OData v4 pomocí webového rozhraní API 2,2</span><span class="sxs-lookup"><span data-stu-id="3688b-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="3688b-104">od Zoe Luo</span><span class="sxs-lookup"><span data-stu-id="3688b-104">by Zoe Luo</span></span>

> <span data-ttu-id="3688b-105">Obvykle by entita mohla být k dispozici pouze v případě, že byla zapouzdřena v sadě entit.</span><span class="sxs-lookup"><span data-stu-id="3688b-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="3688b-106">OData v4 ale nabízí dvě další možnosti, singleton a omezení, z nichž WebAPI 2,2 podporuje.</span><span class="sxs-lookup"><span data-stu-id="3688b-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="3688b-107">Tento článek ukazuje, jak definovat singleton v koncovém bodu OData ve webovém rozhraní API 2,2.</span><span class="sxs-lookup"><span data-stu-id="3688b-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="3688b-108">Informace o tom, co je typu Singleton a jakým způsobem vám jeho používání může přinést, najdete v tématu [použití typu Singleton k definování vaší speciální entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span><span class="sxs-lookup"><span data-stu-id="3688b-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="3688b-109">Informace o vytvoření koncového bodu OData v4 ve webovém rozhraní API najdete v tématu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní api ASP.NET 2,2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="3688b-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="3688b-110">V projektu webového rozhraní API vytvoříme typ singleton pomocí následujícího datového modelu:</span><span class="sxs-lookup"><span data-stu-id="3688b-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![Datový model](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="3688b-112">Typ singleton s názvem `Umbrella` bude definován v závislosti na typu `Company`a v závislosti na typu `Employee`bude definována sada entit s názvem `Employees`.</span><span class="sxs-lookup"><span data-stu-id="3688b-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="3688b-113">Řešení použité v tomto kurzu si můžete stáhnout z [webu CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span><span class="sxs-lookup"><span data-stu-id="3688b-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="3688b-114">Definování datového modelu</span><span class="sxs-lookup"><span data-stu-id="3688b-114">Define the data model</span></span>

1. <span data-ttu-id="3688b-115">Definujte typy CLR.</span><span class="sxs-lookup"><span data-stu-id="3688b-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="3688b-116">Vygenerujte model EDM na základě typů CLR.</span><span class="sxs-lookup"><span data-stu-id="3688b-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="3688b-117">Zde `builder.Singleton<Company>("Umbrella")` instruuje tvůrce modelů, aby vytvořil typ singleton s názvem `Umbrella` v modelu EDM.</span><span class="sxs-lookup"><span data-stu-id="3688b-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="3688b-118">Vygenerovaná metadata budou vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="3688b-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="3688b-119">Z metadat vidíte, že navigační vlastnost `Company` v sadě entit `Employees` je vázána na `Umbrella`typu singleton.</span><span class="sxs-lookup"><span data-stu-id="3688b-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="3688b-120">Vazba je provedena automaticky `ODataConventionModelBuilder`, protože typ `Company` pouze `Umbrella`.</span><span class="sxs-lookup"><span data-stu-id="3688b-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="3688b-121">Pokud v modelu dojde k nejednoznačnosti, můžete použít `HasSingletonBinding` k explicitnímu navázání navigační vlastnosti na typ singleton; `HasSingletonBinding` má stejný účinek jako použití atributu `Singleton` v definici typu CLR:</span><span class="sxs-lookup"><span data-stu-id="3688b-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="3688b-122">Definování typu Singleton Controller</span><span class="sxs-lookup"><span data-stu-id="3688b-122">Define the singleton controller</span></span>

<span data-ttu-id="3688b-123">Podobně jako u řadiče EntitySet zdědí řadič singleton z `ODataController`a název řadiče singleton by měl být `[singletonName]Controller`.</span><span class="sxs-lookup"><span data-stu-id="3688b-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="3688b-124">Aby bylo možné zpracovávat různé druhy požadavků, je nutné v kontroleru předem definovat akce.</span><span class="sxs-lookup"><span data-stu-id="3688b-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="3688b-125">**Směrování atributů** je ve výchozím nastavení povolené v WebApi 2,2.</span><span class="sxs-lookup"><span data-stu-id="3688b-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="3688b-126">Chcete-li například definovat akci pro zpracování dotazů `Revenue` z `Company` pomocí směrování atributů, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="3688b-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="3688b-127">Pokud nejste ochotni definovat atributy pro každou akci, stačí definovat akce, které následují po [konvencích směrování OData](../odata-routing-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="3688b-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="3688b-128">Vzhledem k tomu, že klíč není vyžadován pro dotazování typu Singleton, akce definované v řadiči s jedním odkazem se mírně liší od akcí definovaných v řadiči EntitySet.</span><span class="sxs-lookup"><span data-stu-id="3688b-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="3688b-129">Pro referenci se v seznamu zobrazí signatury metod pro každou definici akce v řadiči s jedním odkazem.</span><span class="sxs-lookup"><span data-stu-id="3688b-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="3688b-130">V podstatě je to vše, co musíte udělat na straně služby.</span><span class="sxs-lookup"><span data-stu-id="3688b-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="3688b-131">[Ukázkový projekt](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) obsahuje veškerý kód pro řešení a klienta OData, který ukazuje, jak použít typ singleton.</span><span class="sxs-lookup"><span data-stu-id="3688b-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="3688b-132">Klient je sestaven podle kroků v části [vytvoření klientské aplikace OData v4](create-an-odata-v4-client-app.md).</span><span class="sxs-lookup"><span data-stu-id="3688b-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="3688b-133">.</span><span class="sxs-lookup"><span data-stu-id="3688b-133">.</span></span> 

<span data-ttu-id="3688b-134">*Díky Leo hu pro původní obsah tohoto článku.*</span><span class="sxs-lookup"><span data-stu-id="3688b-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
