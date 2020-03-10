---
uid: signalr/overview/advanced/dependency-injection
title: Vkládání závislostí v nástroji Signal | Microsoft Docs
author: bradygaster
description: Verze softwaru používané v tomto tématu Visual Studio 2013 k předchozím verzím tohoto tématu v předchozích verzích rozhraní .NET 4,5 Signaler verze 2, kde najdete informace o dřívějších verzích...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537329"
---
# <a name="dependency-injection-in-signalr"></a><span data-ttu-id="2653f-103">Injektáž závislostí v centrech SignalR</span><span class="sxs-lookup"><span data-stu-id="2653f-103">Dependency Injection in SignalR</span></span>

<span data-ttu-id="2653f-104">[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="2653f-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="2653f-105">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="2653f-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="2653f-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2653f-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="2653f-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2653f-107">.NET 4.5</span></span>
> - <span data-ttu-id="2653f-108">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="2653f-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="2653f-109">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="2653f-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="2653f-110">Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="2653f-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="2653f-111">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="2653f-111">Questions and comments</span></span>
>
> <span data-ttu-id="2653f-112">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="2653f-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2653f-113">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="2653f-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="2653f-114">Injektáže závislosti je způsob, jak odebrat pevně kódované závislosti mezi objekty, což usnadňuje nahrazení závislostí objektu buď pro účely testování (pomocí objektů typu), nebo pro změnu chování za běhu.</span><span class="sxs-lookup"><span data-stu-id="2653f-114">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="2653f-115">V tomto kurzu se dozvíte, jak provádět vkládání závislostí na rozbočovačích pro Signal.</span><span class="sxs-lookup"><span data-stu-id="2653f-115">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="2653f-116">Také ukazuje, jak používat kontejnery IoC s nástrojem Signal.</span><span class="sxs-lookup"><span data-stu-id="2653f-116">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="2653f-117">Kontejner IoC je obecná architektura pro vkládání závislostí.</span><span class="sxs-lookup"><span data-stu-id="2653f-117">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="2653f-118">Co je vkládání závislostí?</span><span class="sxs-lookup"><span data-stu-id="2653f-118">What is Dependency Injection?</span></span>

<span data-ttu-id="2653f-119">Pokud jste již obeznámeni se vkládáním závislostí, přeskočte tuto část.</span><span class="sxs-lookup"><span data-stu-id="2653f-119">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="2653f-120">*Vkládání závislostí* (di) je vzor, ve kterém objekty nejsou zodpovědné za vytváření vlastních závislostí.</span><span class="sxs-lookup"><span data-stu-id="2653f-120">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="2653f-121">Tady je jednoduchý příklad pro motivaci DI.</span><span class="sxs-lookup"><span data-stu-id="2653f-121">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="2653f-122">Předpokládejme, že máte objekt, který potřebuje Protokolovat zprávy.</span><span class="sxs-lookup"><span data-stu-id="2653f-122">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="2653f-123">Můžete definovat protokolovací rozhraní:</span><span class="sxs-lookup"><span data-stu-id="2653f-123">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="2653f-124">Ve svém objektu můžete vytvořit `ILogger` pro protokolování zpráv:</span><span class="sxs-lookup"><span data-stu-id="2653f-124">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="2653f-125">To funguje, ale nejedná se o nejlepší návrh.</span><span class="sxs-lookup"><span data-stu-id="2653f-125">This works, but it's not the best design.</span></span> <span data-ttu-id="2653f-126">Pokud chcete nahradit `FileLogger` jinou implementací `ILogger`, budete muset změnit `SomeComponent`.</span><span class="sxs-lookup"><span data-stu-id="2653f-126">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="2653f-127">Supposing, že mnoho dalších objektů používá `FileLogger`, budete je muset změnit.</span><span class="sxs-lookup"><span data-stu-id="2653f-127">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="2653f-128">Nebo pokud se rozhodnete nastavit `FileLogger` typu Singleton, budete také muset provést změny v celé aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2653f-128">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="2653f-129">Lepším přístupem je "vložení" `ILogger` do objektu, například pomocí argumentu konstruktoru:</span><span class="sxs-lookup"><span data-stu-id="2653f-129">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="2653f-130">Nyní objekt není zodpovědný za výběr, který `ILogger` použít.</span><span class="sxs-lookup"><span data-stu-id="2653f-130">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="2653f-131">Můžete přepínat `ILogger` implementace, aniž byste museli měnit objekty, které jsou na ní závislé.</span><span class="sxs-lookup"><span data-stu-id="2653f-131">You can switch `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="2653f-132">Tento model se nazývá [Injektáže konstruktoru](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="2653f-132">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="2653f-133">Dalším vzorem je vkládání pomocí metody Setter, kde můžete nastavit závislost prostřednictvím metody setter nebo vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="2653f-133">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="2653f-134">Jednoduché vkládání závislostí v nástroji Signal</span><span class="sxs-lookup"><span data-stu-id="2653f-134">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="2653f-135">Zvažte aplikaci Chat z kurzu [Začínáme se signálem](../getting-started/tutorial-getting-started-with-signalr.md).</span><span class="sxs-lookup"><span data-stu-id="2653f-135">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="2653f-136">Tady je třída centra z této aplikace:</span><span class="sxs-lookup"><span data-stu-id="2653f-136">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="2653f-137">Předpokládejme, že chcete před odesláním na server uložit zprávy chatu.</span><span class="sxs-lookup"><span data-stu-id="2653f-137">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="2653f-138">Můžete definovat rozhraní, které tuto funkci abstrakce, a použít DI pro vložení rozhraní do třídy `ChatHub`.</span><span class="sxs-lookup"><span data-stu-id="2653f-138">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="2653f-139">Jediným problémem je, že aplikace signalizace nevytváří přímo rozbočovače; Signál je vytvoří za vás.</span><span class="sxs-lookup"><span data-stu-id="2653f-139">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="2653f-140">Ve výchozím nastavení signál očekává, že třída rozbočovače má konstruktor bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="2653f-140">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="2653f-141">Můžete ale snadno zaregistrovat funkci pro vytváření instancí centra a pomocí této funkce provádět DI.</span><span class="sxs-lookup"><span data-stu-id="2653f-141">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="2653f-142">Zaregistrujte funkci voláním **GlobalHost. DependencyResolver. Register**.</span><span class="sxs-lookup"><span data-stu-id="2653f-142">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="2653f-143">Signál Now tuto anonymní funkci vyvolá vždy, když je potřeba vytvořit instanci `ChatHub`.</span><span class="sxs-lookup"><span data-stu-id="2653f-143">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="2653f-144">Kontejnery IoC</span><span class="sxs-lookup"><span data-stu-id="2653f-144">IoC Containers</span></span>

<span data-ttu-id="2653f-145">Předchozí kód je v jednoduchých případech jemný.</span><span class="sxs-lookup"><span data-stu-id="2653f-145">The previous code is fine for simple cases.</span></span> <span data-ttu-id="2653f-146">Ale pořád byste to měli napsat:</span><span class="sxs-lookup"><span data-stu-id="2653f-146">But you still had to write this:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

<span data-ttu-id="2653f-147">Ve složitých aplikacích s mnoha závislostmi může být potřeba napsat spoustu tohoto "" kabelážního "kódu.</span><span class="sxs-lookup"><span data-stu-id="2653f-147">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="2653f-148">Údržbu tohoto kódu může být obtížné, zejména v případě, že jsou závislosti vnořené.</span><span class="sxs-lookup"><span data-stu-id="2653f-148">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="2653f-149">Je také obtížné testování částí.</span><span class="sxs-lookup"><span data-stu-id="2653f-149">It is also hard to unit test.</span></span>

<span data-ttu-id="2653f-150">Jedním z řešení je použít kontejner IoC.</span><span class="sxs-lookup"><span data-stu-id="2653f-150">One solution is to use an IoC container.</span></span> <span data-ttu-id="2653f-151">Kontejner IoC je softwarová součást, která zodpovídá za správu závislostí. Zaregistrujte typy s kontejnerem a potom pomocí kontejneru vytvořte objekty.</span><span class="sxs-lookup"><span data-stu-id="2653f-151">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="2653f-152">Kontejner automaticky vyhodnotí vztahy závislostí.</span><span class="sxs-lookup"><span data-stu-id="2653f-152">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="2653f-153">Mnoho kontejnerů IoC vám také umožňuje řídit objekty, jako je život a rozsah objektu.</span><span class="sxs-lookup"><span data-stu-id="2653f-153">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="2653f-154">"IoC" je zkratka "inverze ovládacího prvku", což je obecný vzor, ve kterém rozhraní volá kód aplikace.</span><span class="sxs-lookup"><span data-stu-id="2653f-154">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="2653f-155">Kontejner IoC sestaví vaše objekty za vás, což "Invertuje" běžný tok řízení.</span><span class="sxs-lookup"><span data-stu-id="2653f-155">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="2653f-156">Používání kontejnerů IoC v nástroji Signal</span><span class="sxs-lookup"><span data-stu-id="2653f-156">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="2653f-157">Aplikace chatu je pravděpodobně příliš jednoduchá a nemůže těžit z kontejneru IoC.</span><span class="sxs-lookup"><span data-stu-id="2653f-157">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="2653f-158">Místo toho se podívejme na ukázku [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) .</span><span class="sxs-lookup"><span data-stu-id="2653f-158">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="2653f-159">Ukázka StockTicker definuje dvě hlavní třídy:</span><span class="sxs-lookup"><span data-stu-id="2653f-159">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="2653f-160">`StockTickerHub`: třída centra, která spravuje připojení klientů.</span><span class="sxs-lookup"><span data-stu-id="2653f-160">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="2653f-161">`StockTicker`: typ singleton, který má skladové ceny a pravidelně je aktualizuje.</span><span class="sxs-lookup"><span data-stu-id="2653f-161">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="2653f-162">`StockTickerHub` drží odkaz na `StockTicker` singleton, zatímco `StockTicker` obsahuje odkaz na **IHubConnectionContext** pro `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="2653f-162">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="2653f-163">Toto rozhraní používá ke komunikaci s `StockTickerHub` instancemi.</span><span class="sxs-lookup"><span data-stu-id="2653f-163">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="2653f-164">(Další informace najdete v tématu [všesměrové vysílání serveru pomocí nástroje ASP.NET Signal](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span><span class="sxs-lookup"><span data-stu-id="2653f-164">(For more information, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).)</span></span>

<span data-ttu-id="2653f-165">Pomocí kontejneru IoC můžete rozplétání tyto závislosti bitu.</span><span class="sxs-lookup"><span data-stu-id="2653f-165">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="2653f-166">Nejprve Zjednodušte `StockTickerHub` a `StockTicker` třídy.</span><span class="sxs-lookup"><span data-stu-id="2653f-166">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="2653f-167">V následujícím kódu jsem zakomentované části, které nepotřebujeme.</span><span class="sxs-lookup"><span data-stu-id="2653f-167">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="2653f-168">Odeberte konstruktor bez parametrů z `StockTickerHub`.</span><span class="sxs-lookup"><span data-stu-id="2653f-168">Remove the parameterless constructor from `StockTickerHub`.</span></span> <span data-ttu-id="2653f-169">Místo toho se k vytvoření centra vždycky používá DI.</span><span class="sxs-lookup"><span data-stu-id="2653f-169">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="2653f-170">V případě StockTicker odeberte instanci typu singleton.</span><span class="sxs-lookup"><span data-stu-id="2653f-170">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="2653f-171">Později použijeme kontejner IoC k řízení životnosti StockTicker.</span><span class="sxs-lookup"><span data-stu-id="2653f-171">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="2653f-172">Také vytvořte konstruktor jako veřejný.</span><span class="sxs-lookup"><span data-stu-id="2653f-172">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="2653f-173">V dalším kroku můžeme kód Refaktorovat vytvořením rozhraní pro `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2653f-173">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="2653f-174">Toto rozhraní použijeme k oddělit `StockTickerHub` od `StockTicker` třídy.</span><span class="sxs-lookup"><span data-stu-id="2653f-174">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="2653f-175">Visual Studio usnadňuje tento druh refaktoringu.</span><span class="sxs-lookup"><span data-stu-id="2653f-175">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="2653f-176">Otevřete soubor StockTicker.cs, klikněte pravým tlačítkem na deklaraci třídy `StockTicker` a vyberte **refaktoring** ... **Rozbalte rozhraní**.</span><span class="sxs-lookup"><span data-stu-id="2653f-176">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="2653f-177">V dialogovém okně **rozbalte rozhraní** klikněte na **Vybrat vše**.</span><span class="sxs-lookup"><span data-stu-id="2653f-177">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="2653f-178">Zbytek ponechte ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="2653f-178">Leave the other defaults.</span></span> <span data-ttu-id="2653f-179">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="2653f-179">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="2653f-180">Visual Studio vytvoří nové rozhraní s názvem `IStockTicker`a také změní `StockTicker` odvodit z `IStockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2653f-180">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="2653f-181">Otevřete soubor IStockTicker.cs a změňte rozhraní na **veřejné**.</span><span class="sxs-lookup"><span data-stu-id="2653f-181">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="2653f-182">Ve třídě `StockTickerHub` změňte dvě instance `StockTicker` na `IStockTicker`:</span><span class="sxs-lookup"><span data-stu-id="2653f-182">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="2653f-183">Vytvoření rozhraní `IStockTicker` není bezpodmínečně nutné, ale chtěl bych ukázat, jak DI může přispět k omezení spojení mezi komponentami v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2653f-183">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="2653f-184">Přidat knihovnu Ninject</span><span class="sxs-lookup"><span data-stu-id="2653f-184">Add the Ninject Library</span></span>

<span data-ttu-id="2653f-185">Existuje mnoho Open Source kontejnerů IoC pro .NET.</span><span class="sxs-lookup"><span data-stu-id="2653f-185">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="2653f-186">V tomto kurzu použijeme [Ninject](http://www.ninject.org/).</span><span class="sxs-lookup"><span data-stu-id="2653f-186">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="2653f-187">(Mezi další oblíbené knihovny patří [Castle Windsor](http://www.castleproject.org/), [Spring.NET](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)a [StructureMap](http://docs.structuremap.net).)</span><span class="sxs-lookup"><span data-stu-id="2653f-187">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="2653f-188">Pomocí Správce balíčků NuGet nainstalujte [knihovnu Ninject](https://nuget.org/packages/Ninject/3.0.1.10).</span><span class="sxs-lookup"><span data-stu-id="2653f-188">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="2653f-189">V aplikaci Visual Studio v nabídce **nástroje** vyberte **správce balíčků NuGet** > **konzolu Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="2653f-189">In Visual Studio, from the **Tools** menu select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="2653f-190">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="2653f-190">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="2653f-191">Výměna překladače závislosti signálu</span><span class="sxs-lookup"><span data-stu-id="2653f-191">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="2653f-192">Chcete-li v rámci signálu Ninject použít, vytvořte třídu, která je odvozena z **DefaultDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="2653f-192">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="2653f-193">Tato třída Přepisuje metody **GetService** a **GetServices** třídy **DefaultDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="2653f-193">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="2653f-194">Signál volá tyto metody k vytvoření různých objektů za běhu, včetně instancí centra, a také různých služeb používaných interně nástrojem Signal.</span><span class="sxs-lookup"><span data-stu-id="2653f-194">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="2653f-195">Metoda **GetService** vytvoří jednu instanci typu.</span><span class="sxs-lookup"><span data-stu-id="2653f-195">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="2653f-196">Přepsat tuto metodu pro volání metody **TryGet** jádra Ninject</span><span class="sxs-lookup"><span data-stu-id="2653f-196">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="2653f-197">Pokud tato metoda vrátí hodnotu null, vraťte se k výchozímu Překladači.</span><span class="sxs-lookup"><span data-stu-id="2653f-197">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="2653f-198">Metoda **GetServices** vytvoří kolekci objektů zadaného typu.</span><span class="sxs-lookup"><span data-stu-id="2653f-198">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="2653f-199">Přepište tuto metodu pro zřetězení výsledků z Ninject s výsledky z výchozího překladače.</span><span class="sxs-lookup"><span data-stu-id="2653f-199">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="2653f-200">Konfigurace vazeb Ninject</span><span class="sxs-lookup"><span data-stu-id="2653f-200">Configure Ninject Bindings</span></span>

<span data-ttu-id="2653f-201">Nyní použijeme Ninject k deklarování vazeb typů.</span><span class="sxs-lookup"><span data-stu-id="2653f-201">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="2653f-202">Otevřete třídu Startup.cs vaší aplikace (vytvořenou ručně podle pokynů pro balíček v tématu `readme.txt`nebo vytvořeného přidáním ověřování do projektu).</span><span class="sxs-lookup"><span data-stu-id="2653f-202">Open your application's Startup.cs class (that you either created manually as per the package instructions in `readme.txt`, or that was created by adding authentication to your project).</span></span> <span data-ttu-id="2653f-203">V metodě `Startup.Configuration` vytvořte kontejner Ninject, který Ninject volá *jádro*.</span><span class="sxs-lookup"><span data-stu-id="2653f-203">In the `Startup.Configuration` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="2653f-204">Vytvořte instanci našeho vlastního překladače závislosti:</span><span class="sxs-lookup"><span data-stu-id="2653f-204">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="2653f-205">Vytvořte vazbu pro `IStockTicker` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="2653f-205">Create a binding for `IStockTicker` as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

<span data-ttu-id="2653f-206">Tento kód říká dvě věci.</span><span class="sxs-lookup"><span data-stu-id="2653f-206">This code is saying two things.</span></span> <span data-ttu-id="2653f-207">Nejprve, kdykoli aplikace potřebuje `IStockTicker`, by jádro mělo vytvořit instanci `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2653f-207">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="2653f-208">Druhý, třída `StockTicker` by měla být vytvořená jako objekt typu singleton.</span><span class="sxs-lookup"><span data-stu-id="2653f-208">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="2653f-209">Ninject vytvoří jednu instanci objektu a vrátí stejnou instanci pro každý požadavek.</span><span class="sxs-lookup"><span data-stu-id="2653f-209">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="2653f-210">Vytvořte vazbu pro **IHubConnectionContext** následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="2653f-210">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="2653f-211">Tento kód vytvoří anonymní funkci, která vrátí **IHubConnection**.</span><span class="sxs-lookup"><span data-stu-id="2653f-211">This code creates an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="2653f-212">Metoda **WhenInjectedInto** přikáže Ninject, aby tuto funkci používala pouze při vytváření instancí `IStockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2653f-212">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="2653f-213">Důvodem je, že signál vytváří instance **IHubConnectionContext** interně a nechceme přepsat způsob, jakým ho signál vytvoří.</span><span class="sxs-lookup"><span data-stu-id="2653f-213">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="2653f-214">Tato funkce se vztahuje pouze na naši třídu `StockTicker`.</span><span class="sxs-lookup"><span data-stu-id="2653f-214">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="2653f-215">Předání překladače závislosti do metody **MapSignalR** přidáním konfigurace centra:</span><span class="sxs-lookup"><span data-stu-id="2653f-215">Pass the dependency resolver into the **MapSignalR** method by adding a hub configuration:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="2653f-216">Aktualizujte metodu Startup. ConfigureSignalR ve spouštěcí třídě ukázky s novým parametrem:</span><span class="sxs-lookup"><span data-stu-id="2653f-216">Update the Startup.ConfigureSignalR method in the sample's Startup class with the new parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="2653f-217">Nyní bude signál používat překladač zadaný v **MapSignalR**namísto výchozího překladače.</span><span class="sxs-lookup"><span data-stu-id="2653f-217">Now SignalR will use the resolver specified in **MapSignalR**, instead of the default resolver.</span></span>

<span data-ttu-id="2653f-218">Zde je kompletní výpis kódu pro `Startup.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="2653f-218">Here is the complete code listing for `Startup.Configuration`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

<span data-ttu-id="2653f-219">Chcete-li spustit aplikaci StockTicker v aplikaci Visual Studio, stiskněte klávesu F5.</span><span class="sxs-lookup"><span data-stu-id="2653f-219">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="2653f-220">V okně prohlížeče přejděte na `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span><span class="sxs-lookup"><span data-stu-id="2653f-220">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="2653f-221">Aplikace má naprosto stejné funkce jako předtím.</span><span class="sxs-lookup"><span data-stu-id="2653f-221">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="2653f-222">(Popis najdete v tématu [vysílání serveru pomocí nástroje ASP.NET Signal](../getting-started/tutorial-server-broadcast-with-signalr.md).) Nezměnili jsme chování. Právě jsme usnadnili testování, údržbu a vývoj kódu.</span><span class="sxs-lookup"><span data-stu-id="2653f-222">(For a description, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
