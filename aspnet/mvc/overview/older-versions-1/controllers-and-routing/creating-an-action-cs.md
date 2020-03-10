---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Vytvoření akce (C#) | Microsoft Docs
author: microsoft
description: Přečtěte si, jak přidat novou akci k řadiči ASP.NET MVC. Seznamte se s požadavky na metodu, která může být akcí.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582052"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="0f990-104">Vytvoření akce (C#)</span><span class="sxs-lookup"><span data-stu-id="0f990-104">Creating an Action (C#)</span></span>

<span data-ttu-id="0f990-105">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0f990-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0f990-106">Přečtěte si, jak přidat novou akci k řadiči ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="0f990-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="0f990-107">Seznamte se s požadavky na metodu, která může být akcí.</span><span class="sxs-lookup"><span data-stu-id="0f990-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="0f990-108">Cílem tohoto kurzu je vysvětlit, jak můžete vytvořit novou akci kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0f990-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="0f990-109">Získáte informace o požadavcích metody akce.</span><span class="sxs-lookup"><span data-stu-id="0f990-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="0f990-110">Naučíte se také, jak zabránit tomu, aby byla metoda vystavena jako akce.</span><span class="sxs-lookup"><span data-stu-id="0f990-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="0f990-111">Přidání akce do kontroleru</span><span class="sxs-lookup"><span data-stu-id="0f990-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="0f990-112">Přidáte novou akci do kontroleru přidáním nové metody do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0f990-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="0f990-113">Například kontroler v výpisu 1 obsahuje akci s názvem index () a akci s názvem SayHello ().</span><span class="sxs-lookup"><span data-stu-id="0f990-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="0f990-114">Obě metody jsou zpřístupněny jako akce.</span><span class="sxs-lookup"><span data-stu-id="0f990-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="0f990-115">**Výpis 1 – souboru controllers\homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="0f990-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="0f990-116">Aby bylo možné zveřejnit celému základnímu objektu jako akci, metoda musí splňovat určité požadavky:</span><span class="sxs-lookup"><span data-stu-id="0f990-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="0f990-117">Metoda musí být veřejná.</span><span class="sxs-lookup"><span data-stu-id="0f990-117">The method must be public.</span></span>
- <span data-ttu-id="0f990-118">Metoda nemůže být statickou metodou.</span><span class="sxs-lookup"><span data-stu-id="0f990-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="0f990-119">Metoda nemůže být metodou rozšíření.</span><span class="sxs-lookup"><span data-stu-id="0f990-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="0f990-120">Metoda nemůže být konstruktor, getter nebo setter.</span><span class="sxs-lookup"><span data-stu-id="0f990-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="0f990-121">Metoda nemůže mít otevřené obecné typy.</span><span class="sxs-lookup"><span data-stu-id="0f990-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="0f990-122">Metoda není metodou základní třídy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0f990-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="0f990-123">Metoda nemůže obsahovat parametry **ref** nebo **out** .</span><span class="sxs-lookup"><span data-stu-id="0f990-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="0f990-124">Všimněte si, že pro návratový typ akce kontroleru neexistují žádná omezení.</span><span class="sxs-lookup"><span data-stu-id="0f990-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="0f990-125">Akce kontroleru může vracet řetězec, datum a čas, instanci náhodné třídy nebo void.</span><span class="sxs-lookup"><span data-stu-id="0f990-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="0f990-126">Rozhraní ASP.NET MVC převede libovolný návratový typ, který není výsledkem akce, do řetězce a vykreslí řetězec do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="0f990-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="0f990-127">Když přidáte libovolnou metodu, která porušuje tyto požadavky na kontroler, je metoda vystavena jako akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="0f990-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="0f990-128">Buďte opatrní.</span><span class="sxs-lookup"><span data-stu-id="0f990-128">Be careful here.</span></span> <span data-ttu-id="0f990-129">Akci kontroleru může vyvolat kdokoli připojený k Internetu.</span><span class="sxs-lookup"><span data-stu-id="0f990-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="0f990-130">Nevytvářejte například akci kontroleru DeleteMyWebsite ().</span><span class="sxs-lookup"><span data-stu-id="0f990-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="0f990-131">Zabránění vyvolání veřejné metody</span><span class="sxs-lookup"><span data-stu-id="0f990-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="0f990-132">Pokud potřebujete vytvořit veřejnou metodu ve třídě kontroleru a nechcete ji zveřejnit jako akci kontroleru, můžete zabránit vyvolání metody pomocí atributu [neaction].</span><span class="sxs-lookup"><span data-stu-id="0f990-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="0f990-133">Například kontroler v seznamu 2 obsahuje veřejnou metodu s názvem CompanySecrets (), která je upravena atributem [neaction].</span><span class="sxs-lookup"><span data-stu-id="0f990-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="0f990-134">**Výpis 2 – Controllers\WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="0f990-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="0f990-135">Pokud se pokusíte vyvolat akci kontroleru CompanySecrets () tak, že do panelu Adresa v prohlížeči zadáte/Work/CompanySecrets, zobrazí se chybová zpráva na obrázku 1.</span><span class="sxs-lookup"><span data-stu-id="0f990-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="0f990-136">[![vyvolání metody nečinnosti](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0f990-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="0f990-137">**Obrázek 01**: vyvolání metody nečinnosti ([kliknutím zobrazíte obrázek v plné velikosti](creating-an-action-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="0f990-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0f990-138">[Předchozí](creating-a-controller-cs.md)
> [Další](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0f990-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
