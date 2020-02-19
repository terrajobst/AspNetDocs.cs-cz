---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dynamické zobrazení vs. Zobrazení silného typu | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3e81c6381b1e280e3b74cb7eb6ea6e6c3224e655
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455646"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="188f0-103">Dynamické zobrazení vs.</span><span class="sxs-lookup"><span data-stu-id="188f0-103">Dynamic v.</span></span> <span data-ttu-id="188f0-104">zobrazení se silnými typy</span><span class="sxs-lookup"><span data-stu-id="188f0-104">Strongly Typed Views</span></span>

<span data-ttu-id="188f0-105">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="188f0-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="188f0-106">Existují tři způsoby, jak předat informace z kontroleru k zobrazení v ASP.NET MVC 3:</span><span class="sxs-lookup"><span data-stu-id="188f0-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="188f0-107">Jako objekt modelu silného typu.</span><span class="sxs-lookup"><span data-stu-id="188f0-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="188f0-108">Jako dynamický typ (pomocí @model Dynamic)</span><span class="sxs-lookup"><span data-stu-id="188f0-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="188f0-109">Použití ViewBag</span><span class="sxs-lookup"><span data-stu-id="188f0-109">Using the ViewBag</span></span>

<span data-ttu-id="188f0-110">Napsal (a) jsem jednoduchou přední aplikaci MVC 3 k porovnání a kontrastu dynamických a silných zobrazení typu.</span><span class="sxs-lookup"><span data-stu-id="188f0-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="188f0-111">Kontroler začíná jednoduchým seznamem blogů:</span><span class="sxs-lookup"><span data-stu-id="188f0-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="188f0-112">Klikněte pravým tlačítkem na metodu IndexNotStonglyTyped () a přidejte zobrazení Razor.</span><span class="sxs-lookup"><span data-stu-id="188f0-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="188f0-113">[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="188f0-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="188f0-114">Ujistěte se, že není zaškrtnuto políčko **vytvořit zobrazení silného typu** .</span><span class="sxs-lookup"><span data-stu-id="188f0-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="188f0-115">Výsledný pohled neobsahuje mnohem:</span><span class="sxs-lookup"><span data-stu-id="188f0-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="188f0-116">Vzhledem k tomu, že používáme dynamické a nesilné zobrazení, IntelliSense nám to nepomůže.</span><span class="sxs-lookup"><span data-stu-id="188f0-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="188f0-117">Dokončený kód je zobrazen níže:</span><span class="sxs-lookup"><span data-stu-id="188f0-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="188f0-118">[![6646. NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="188f0-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="188f0-119">Nyní přidáme zobrazení silného typu.</span><span class="sxs-lookup"><span data-stu-id="188f0-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="188f0-120">Do kontroleru přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="188f0-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

<span data-ttu-id="188f0-121">Všimněte si, že je přesně stejný návratový pohled (topBlogs); volání jako zobrazení bez silného typu.</span><span class="sxs-lookup"><span data-stu-id="188f0-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="188f0-122">Klikněte pravým tlačítkem myši v *StonglyTypedIndex ()* a vyberte **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="188f0-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="188f0-123">Tentokrát vyberte třídu modelu **blogu** a vyberte **seznam** jako šablonu generování uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="188f0-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="188f0-124">[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="188f0-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="188f0-125">V nové šabloně zobrazení získáme podporu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="188f0-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="188f0-126">[![7002. IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="188f0-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>

<span data-ttu-id="188f0-127">Projekt c# se dá stáhnout [tady](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span><span class="sxs-lookup"><span data-stu-id="188f0-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
