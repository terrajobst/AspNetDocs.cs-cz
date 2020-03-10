---
uid: signalr/overview/older-versions/dependency-injection
title: Vkládání závislostí v návěsti 1. x | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: de838ab6b3a299eb1e5ebeb9fa3c583478ce3e56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536951"
---
# <a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="6d827-102">Injektáž závislostí v centrech SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="6d827-102">Dependency Injection in SignalR 1.x</span></span>

<span data-ttu-id="6d827-103">[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="6d827-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="6d827-104">Injektáže závislosti je způsob, jak odebrat pevně kódované závislosti mezi objekty, což usnadňuje nahrazení závislostí objektu buď pro účely testování (pomocí objektů typu), nebo pro změnu chování za běhu.</span><span class="sxs-lookup"><span data-stu-id="6d827-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="6d827-105">V tomto kurzu se dozvíte, jak provádět vkládání závislostí na rozbočovačích pro Signal.</span><span class="sxs-lookup"><span data-stu-id="6d827-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="6d827-106">Také ukazuje, jak používat kontejnery IoC s nástrojem Signal.</span><span class="sxs-lookup"><span data-stu-id="6d827-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="6d827-107">Kontejner IoC je obecná architektura pro vkládání závislostí.</span><span class="sxs-lookup"><span data-stu-id="6d827-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="6d827-108">Co je vkládání závislostí?</span><span class="sxs-lookup"><span data-stu-id="6d827-108">What is Dependency Injection?</span></span>

<span data-ttu-id="6d827-109">Pokud jste již obeznámeni se vkládáním závislostí, přeskočte tuto část.</span><span class="sxs-lookup"><span data-stu-id="6d827-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="6d827-110">*Vkládání závislostí* (di) je vzor, ve kterém objekty nejsou zodpovědné za vytváření vlastních závislostí.</span><span class="sxs-lookup"><span data-stu-id="6d827-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="6d827-111">Tady je jednoduchý příklad pro motivaci DI.</span><span class="sxs-lookup"><span data-stu-id="6d827-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="6d827-112">Předpokládejme, že máte objekt, který potřebuje Protokolovat zprávy.</span><span class="sxs-lookup"><span data-stu-id="6d827-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="6d827-113">Můžete definovat protokolovací rozhraní:</span><span class="sxs-lookup"><span data-stu-id="6d827-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="6d827-114">Ve svém objektu můžete vytvořit `ILogger` pro protokolování zpráv:</span><span class="sxs-lookup"><span data-stu-id="6d827-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="6d827-115">To funguje, ale nejedná se o nejlepší návrh.</span><span class="sxs-lookup"><span data-stu-id="6d827-115">This works, but it's not the best design.</span></span> <span data-ttu-id="6d827-116">Pokud chcete nahradit `FileLogger` jinou implementací `ILogger`, budete muset změnit `SomeComponent`.</span><span class="sxs-lookup"><span data-stu-id="6d827-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="6d827-117">Supposing, že mnoho dalších objektů používá `FileLogger`, budete je muset změnit.</span><span class="sxs-lookup"><span data-stu-id="6d827-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="6d827-118">Nebo pokud se rozhodnete nastavit `FileLogger` typu Singleton, budete také muset provést změny v celé aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6d827-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="6d827-119">Lepším přístupem je "vložení" `ILogger` do objektu, například pomocí argumentu konstruktoru:</span><span class="sxs-lookup"><span data-stu-id="6d827-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="6d827-120">Nyní objekt není zodpovědný za výběr, který `ILogger` použít.</span><span class="sxs-lookup"><span data-stu-id="6d827-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="6d827-121">Můžete přepínat `ILogger` implementace, aniž byste museli měnit objekty, které jsou na ní závislé.</span><span class="sxs-lookup"><span data-stu-id="6d827-121">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="6d827-122">Tento model se nazývá [Injektáže konstruktoru](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="6d827-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="6d827-123">Dalším vzorem je vkládání pomocí metody Setter, kde můžete nastavit závislost prostřednictvím metody setter nebo vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6d827-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="6d827-124">Jednoduché vkládání závislostí v nástroji Signal</span><span class="sxs-lookup"><span data-stu-id="6d827-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="6d827-125">Zvažte aplikaci Chat z kurzu [Začínáme se signálem](../getting-started/tutorial-getting-started-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="6d827-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="6d827-126">Tady je třída centra z této aplikace:</span><span class="sxs-lookup"><span data-stu-id="6d827-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="6d827-127">Předpokládejme, že chcete před odesláním na server uložit zprávy chatu.</span><span class="sxs-lookup"><span data-stu-id="6d827-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="6d827-128">Můžete definovat rozhraní, které tuto funkci abstrakce, a použít DI pro vložení rozhraní do třídy `ChatHub`.</span><span class="sxs-lookup"><span data-stu-id="6d827-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="6d827-129">Jediným problémem je, že aplikace signalizace nevytváří přímo rozbočovače; Signál je vytvoří za vás.</span><span class="sxs-lookup"><span data-stu-id="6d827-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="6d827-130">Ve výchozím nastavení signál očekává, že třída rozbočovače má konstruktor bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="6d827-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="6d827-131">Můžete ale snadno zaregistrovat funkci pro vytváření instancí centra a pomocí této funkce provádět DI.</span><span class="sxs-lookup"><span data-stu-id="6d827-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="6d827-132">Zaregistrujte funkci voláním **GlobalHost. DependencyResolver. Register**.</span><span class="sxs-lookup"><span data-stu-id="6d827-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="6d827-133">Signál Now tuto anonymní funkci vyvolá vždy, když je potřeba vytvořit instanci `ChatHub`.</span><span class="sxs-lookup"><span data-stu-id="6d827-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="6d827-134">Kontejnery IoC</span><span class="sxs-lookup"><span data-stu-id="6d827-134">IoC Containers</span></span>

<span data-ttu-id="6d827-135">Předchozí kód je v jednoduchých případech jemný.</span><span class="sxs-lookup"><span data-stu-id="6d827-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="6d827-136">Ale pořád byste to měli napsat:</span><span class="sxs-lookup"><span data-stu-id="6d827-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="6d827-137">Ve složitých aplikacích s mnoha závislostmi může být potřeba napsat spoustu tohoto "" kabelážního "kódu.</span><span class="sxs-lookup"><span data-stu-id="6d827-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="6d827-138">Údržbu tohoto kódu může být obtížné, zejména v případě, že jsou závislosti vnořené.</span><span class="sxs-lookup"><span data-stu-id="6d827-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="6d827-139">Je také obtížné testování částí.</span><span class="sxs-lookup"><span data-stu-id="6d827-139">It is also hard to unit test.</span></span>

<span data-ttu-id="6d827-140">Jedním z řešení je použít kontejner IoC.</span><span class="sxs-lookup"><span data-stu-id="6d827-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="6d827-141">Kontejner IoC je softwarová součást, která zodpovídá za správu závislostí. Zaregistrujte typy s kontejnerem a potom pomocí kontejneru vytvořte objekty.</span><span class="sxs-lookup"><span data-stu-id="6d827-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="6d827-142">Kontejner automaticky vyhodnotí vztahy závislostí.</span><span class="sxs-lookup"><span data-stu-id="6d827-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="6d827-143">Mnoho kontejnerů IoC vám také umožňuje řídit objekty, jako je život a rozsah objektu.</span><span class="sxs-lookup"><span data-stu-id="6d827-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="6d827-144">"IoC" je zkratka "inverze ovládacího prvku", což je obecný vzor, ve kterém rozhraní volá kód aplikace.</span><span class="sxs-lookup"><span data-stu-id="6d827-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="6d827-145">Kontejner IoC sestaví vaše objekty za vás, což "Invertuje" běžný tok řízení.</span><span class="sxs-lookup"><span data-stu-id="6d827-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="6d827-146">Používání kontejnerů IoC v nástroji Signal</span><span class="sxs-lookup"><span data-stu-id="6d827-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="6d827-147">Aplikace chatu je pravděpodobně příliš jednoduchá a nemůže těžit z kontejneru IoC.</span><span class="sxs-lookup"><span data-stu-id="6d827-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="6d827-148">Místo toho se podívejme na ukázku [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) .</span><span class="sxs-lookup"><span data-stu-id="6d827-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="6d827-149">Ukázka StockTicker definuje dvě hlavní třídy:</span><span class="sxs-lookup"><span data-stu-id="6d827-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="6d827-150">`StockTickerHub`: třída centra, která spravuje připojení klientů.</span><span class="sxs-lookup"><span data-stu-id="6d827-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="6d827-151">`StockTicker`: typ singleton, který má skladové ceny a pravidelně je aktualizuje.</span><span class="sxs-lookup"><span data-stu-id="6d827-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="6d827-152">`StockTickerHub` drží odkaz na `StockTicker` singleton, zatímco `StockTicker` obsahuje odkaz na **IHubConnectionContext** pro `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="6d827-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="6d827-153">Toto rozhraní používá ke komunikaci s `StockTickerHub` instancemi.</span><span class="sxs-lookup"><span data-stu-id="6d827-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="6d827-154">(Další informace najdete v tématu [všesměrové vysílání serveru pomocí nástroje ASP.NET Signal](index.md).)</span><span class="sxs-lookup"><span data-stu-id="6d827-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="6d827-155">Pomocí kontejneru IoC můžete rozplétání tyto závislosti bitu.</span><span class="sxs-lookup"><span data-stu-id="6d827-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="6d827-156">Nejprve Zjednodušte `StockTickerHub` a `StockTicker` třídy.</span><span class="sxs-lookup"><span data-stu-id="6d827-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="6d827-157">V následujícím kódu jsem zakomentované části, které nepotřebujeme.</span><span class="sxs-lookup"><span data-stu-id="6d827-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="6d827-158">Odeberte konstruktor bez parametrů z `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="6d827-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="6d827-159">Místo toho se k vytvoření centra vždycky používá DI.</span><span class="sxs-lookup"><span data-stu-id="6d827-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="6d827-160">V případě StockTicker odeberte instanci typu singleton.</span><span class="sxs-lookup"><span data-stu-id="6d827-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="6d827-161">Později použijeme kontejner IoC k řízení životnosti StockTicker.</span><span class="sxs-lookup"><span data-stu-id="6d827-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="6d827-162">Také vytvořte konstruktor jako veřejný.</span><span class="sxs-lookup"><span data-stu-id="6d827-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="6d827-163">V dalším kroku můžeme kód Refaktorovat vytvořením rozhraní pro `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="6d827-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="6d827-164">Toto rozhraní použijeme k oddělit `StockTickerHub` od `StockTicker` třídy.</span><span class="sxs-lookup"><span data-stu-id="6d827-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="6d827-165">Visual Studio usnadňuje tento druh refaktoringu.</span><span class="sxs-lookup"><span data-stu-id="6d827-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="6d827-166">Otevřete soubor StockTicker.cs, klikněte pravým tlačítkem na deklaraci třídy `StockTicker` a vyberte **refaktoring** ... **Rozbalte rozhraní**.</span><span class="sxs-lookup"><span data-stu-id="6d827-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="6d827-167">V dialogovém okně **rozbalte rozhraní** klikněte na **Vybrat vše**.</span><span class="sxs-lookup"><span data-stu-id="6d827-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="6d827-168">Zbytek ponechte ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="6d827-168">Leave the other defaults.</span></span> <span data-ttu-id="6d827-169">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d827-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="6d827-170">Visual Studio vytvoří nové rozhraní s názvem `IStockTicker`a také změní `StockTicker` odvodit z `IStockTicker`.</span><span class="sxs-lookup"><span data-stu-id="6d827-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="6d827-171">Otevřete soubor IStockTicker.cs a změňte rozhraní na **veřejné**.</span><span class="sxs-lookup"><span data-stu-id="6d827-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="6d827-172">Ve třídě `StockTickerHub` změňte dvě instance `StockTicker` na `IStockTicker`:</span><span class="sxs-lookup"><span data-stu-id="6d827-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="6d827-173">Vytvoření rozhraní `IStockTicker` není bezpodmínečně nutné, ale chtěl bych ukázat, jak DI může přispět k omezení spojení mezi komponentami v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="6d827-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="6d827-174">Přidat knihovnu Ninject</span><span class="sxs-lookup"><span data-stu-id="6d827-174">Add the Ninject Library</span></span>

<span data-ttu-id="6d827-175">Existuje mnoho Open Source kontejnerů IoC pro .NET.</span><span class="sxs-lookup"><span data-stu-id="6d827-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="6d827-176">V tomto kurzu použijeme [Ninject](http://www.ninject.org/).</span><span class="sxs-lookup"><span data-stu-id="6d827-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="6d827-177">(Mezi další oblíbené knihovny patří [Castle Windsor](http://www.castleproject.org/), [Spring.NET](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)a [StructureMap](http://docs.structuremap.net).)</span><span class="sxs-lookup"><span data-stu-id="6d827-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="6d827-178">Pomocí Správce balíčků NuGet nainstalujte [knihovnu Ninject](https://nuget.org/packages/Ninject/3.0.1.10).</span><span class="sxs-lookup"><span data-stu-id="6d827-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="6d827-179">V aplikaci Visual Studio v nabídce **nástroje** vyberte **správce balíčků NuGet** > **konzolu Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="6d827-179">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="6d827-180">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="6d827-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="6d827-181">Výměna překladače závislosti signálu</span><span class="sxs-lookup"><span data-stu-id="6d827-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="6d827-182">Chcete-li v rámci signálu Ninject použít, vytvořte třídu, která je odvozena z **DefaultDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="6d827-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="6d827-183">Tato třída Přepisuje metody **GetService** a **GetServices** třídy **DefaultDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="6d827-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="6d827-184">Signál volá tyto metody k vytvoření různých objektů za běhu, včetně instancí centra, a také různých služeb používaných interně nástrojem Signal.</span><span class="sxs-lookup"><span data-stu-id="6d827-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="6d827-185">Metoda **GetService** vytvoří jednu instanci typu.</span><span class="sxs-lookup"><span data-stu-id="6d827-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="6d827-186">Přepsat tuto metodu pro volání metody **TryGet** jádra Ninject</span><span class="sxs-lookup"><span data-stu-id="6d827-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="6d827-187">Pokud tato metoda vrátí hodnotu null, vraťte se k výchozímu Překladači.</span><span class="sxs-lookup"><span data-stu-id="6d827-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="6d827-188">Metoda **GetServices** vytvoří kolekci objektů zadaného typu.</span><span class="sxs-lookup"><span data-stu-id="6d827-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="6d827-189">Přepište tuto metodu pro zřetězení výsledků z Ninject s výsledky z výchozího překladače.</span><span class="sxs-lookup"><span data-stu-id="6d827-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="6d827-190">Konfigurace vazeb Ninject</span><span class="sxs-lookup"><span data-stu-id="6d827-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="6d827-191">Nyní použijeme Ninject k deklarování vazeb typů.</span><span class="sxs-lookup"><span data-stu-id="6d827-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="6d827-192">Otevřete soubor RegisterHubs.cs.</span><span class="sxs-lookup"><span data-stu-id="6d827-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="6d827-193">V metodě `RegisterHubs.Start` vytvořte kontejner Ninject, který Ninject volá *jádro*.</span><span class="sxs-lookup"><span data-stu-id="6d827-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="6d827-194">Vytvořte instanci našeho vlastního překladače závislosti:</span><span class="sxs-lookup"><span data-stu-id="6d827-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="6d827-195">Vytvořte vazbu pro `IStockTicker` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="6d827-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="6d827-196">Tento kód říká dvě věci.</span><span class="sxs-lookup"><span data-stu-id="6d827-196">This code is saying two things.</span></span> <span data-ttu-id="6d827-197">Nejprve, kdykoli aplikace potřebuje `IStockTicker`, by jádro mělo vytvořit instanci `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="6d827-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="6d827-198">Druhý, třída `StockTicker` by měla být vytvořená jako objekt typu singleton.</span><span class="sxs-lookup"><span data-stu-id="6d827-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="6d827-199">Ninject vytvoří jednu instanci objektu a vrátí stejnou instanci pro každý požadavek.</span><span class="sxs-lookup"><span data-stu-id="6d827-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="6d827-200">Vytvořte vazbu pro **IHubConnectionContext** následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="6d827-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="6d827-201">Tento kód vytvoří anonymní funkci, která vrátí **IHubConnection**.</span><span class="sxs-lookup"><span data-stu-id="6d827-201">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="6d827-202">Metoda **WhenInjectedInto** přikáže Ninject, aby tuto funkci používala pouze při vytváření instancí `IStockTicker`.</span><span class="sxs-lookup"><span data-stu-id="6d827-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="6d827-203">Důvodem je, že signál vytváří instance **IHubConnectionContext** interně a nechceme přepsat způsob, jakým ho signál vytvoří.</span><span class="sxs-lookup"><span data-stu-id="6d827-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="6d827-204">Tato funkce se vztahuje pouze na naši třídu `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="6d827-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="6d827-205">Předejte překladač závislosti do metody **MapHubs** :</span><span class="sxs-lookup"><span data-stu-id="6d827-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="6d827-206">Nyní bude signál používat překladač zadaný v **MapHubs**namísto výchozího překladače.</span><span class="sxs-lookup"><span data-stu-id="6d827-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="6d827-207">Zde je kompletní výpis kódu pro `RegisterHubs.Start`.</span><span class="sxs-lookup"><span data-stu-id="6d827-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="6d827-208">Chcete-li spustit aplikaci StockTicker v aplikaci Visual Studio, stiskněte klávesu F5.</span><span class="sxs-lookup"><span data-stu-id="6d827-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="6d827-209">V okně prohlížeče přejděte na `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span><span class="sxs-lookup"><span data-stu-id="6d827-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="6d827-210">Aplikace má naprosto stejné funkce jako předtím.</span><span class="sxs-lookup"><span data-stu-id="6d827-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="6d827-211">(Popis najdete v tématu [vysílání serveru pomocí nástroje ASP.NET Signal](index.md).) Nezměnili jsme chování. Právě jsme usnadnili testování, údržbu a vývoj kódu.</span><span class="sxs-lookup"><span data-stu-id="6d827-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
