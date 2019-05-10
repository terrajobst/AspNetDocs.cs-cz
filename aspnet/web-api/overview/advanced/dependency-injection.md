---
uid: web-api/overview/advanced/dependency-injection
title: Injektáž závislostí v rozhraní ASP.NET Web API 2 – ASP.NET 4.x
author: MikeWasson
description: Tento kurz ukazuje postupy při vložení závislosti do řadiče rozhraní ASP.NET Web API pro ASP.NET 4.x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 138ccb5800e801d382c11e3989ec3e3c074a79fe
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115706"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="7b446-103">Injektáž závislostí v rozhraní ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="7b446-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="7b446-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7b446-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7b446-105">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="7b446-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="7b446-106">Tento kurz ukazuje postupy při vložení závislosti do vašeho kontroleru webového rozhraní API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7b446-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7b446-107">V tomto kurzu použili verze softwaru</span><span class="sxs-lookup"><span data-stu-id="7b446-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7b446-108">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="7b446-108">Web API 2</span></span>
> - [<span data-ttu-id="7b446-109">Blok aplikací Unity</span><span class="sxs-lookup"><span data-stu-id="7b446-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="7b446-110">Entity Framework 6 (verze 5 taky funguje)</span><span class="sxs-lookup"><span data-stu-id="7b446-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="7b446-111">Co je injektáž závislostí?</span><span class="sxs-lookup"><span data-stu-id="7b446-111">What is Dependency Injection?</span></span>

<span data-ttu-id="7b446-112">*Závislost* je libovolný objekt, který je vyžadován jiným objektem.</span><span class="sxs-lookup"><span data-stu-id="7b446-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="7b446-113">Například je společné pro definování [úložiště](http://martinfowler.com/eaaCatalog/repository.html) přístup k datům, která zpracovává.</span><span class="sxs-lookup"><span data-stu-id="7b446-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="7b446-114">Pojďme ukazuje příklad.</span><span class="sxs-lookup"><span data-stu-id="7b446-114">Let's illustrate with an example.</span></span> <span data-ttu-id="7b446-115">Nejprve budeme definovat model domény:</span><span class="sxs-lookup"><span data-stu-id="7b446-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="7b446-116">Tady je jednoduché úložiště třídu, která ukládá položky v databázi pomocí Entity Frameworku.</span><span class="sxs-lookup"><span data-stu-id="7b446-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="7b446-117">Teď nadefinujeme kontroler Web API, který podporuje požadavky GET pro `Product` entity.</span><span class="sxs-lookup"><span data-stu-id="7b446-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="7b446-118">(I jsem vynecháním POST a další metody pro zjednodušení.) Zde je první pokus o:</span><span class="sxs-lookup"><span data-stu-id="7b446-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="7b446-119">Všimněte si, že třída kontroleru závisí na `ProductRepository`, a vytvoření kontroleru, dáváme `ProductRepository` instance.</span><span class="sxs-lookup"><span data-stu-id="7b446-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="7b446-120">Je však vhodné pevný kód závislosti tímto způsobem z několika důvodů.</span><span class="sxs-lookup"><span data-stu-id="7b446-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="7b446-121">Pokud budete chtít nahradit `ProductRepository` s jinou implementaci, budete také muset upravit třídy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7b446-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="7b446-122">Pokud `ProductRepository` má závislosti, je nutné nakonfigurovat tyto uvnitř kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7b446-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="7b446-123">Pro projekt velkých s více řadiči změní váš kód konfigurace rozmístěny na váš projekt.</span><span class="sxs-lookup"><span data-stu-id="7b446-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="7b446-124">Je těžké test jednotky, protože kontroler je pevně zakódovaný k dotazování databáze.</span><span class="sxs-lookup"><span data-stu-id="7b446-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="7b446-125">Pro testování částí měli byste použít model nebo zástupné procedury úložiště, které není možné s aktuální návrhu.</span><span class="sxs-lookup"><span data-stu-id="7b446-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="7b446-126">Jsme řešení těchto problémů podle *vkládá* úložiště do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7b446-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="7b446-127">Nejprve Refaktorovat `ProductRepository` třídy do rozhraní:</span><span class="sxs-lookup"><span data-stu-id="7b446-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="7b446-128">Zadejte `IProductRepository` jako parametr konstruktoru:</span><span class="sxs-lookup"><span data-stu-id="7b446-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="7b446-129">Tento příklad používá [konstruktor vkládání](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="7b446-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="7b446-130">Můžete také použít *setter vkládání*, kde nastavujete závislost prostřednictvím metody setter nebo vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="7b446-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="7b446-131">Ale nyní je nějaký problém, protože aplikace přímo nevytváří kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7b446-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="7b446-132">Webové rozhraní API vytvoří kontroler při směruje žádosti a webového rozhraní API neví nic o `IProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="7b446-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="7b446-133">To přichází překladač závislostí webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="7b446-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="7b446-134">Překladač závislostí webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="7b446-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="7b446-135">Definuje webového rozhraní API **IDependencyResolver** rozhraní pro vyřešení závislostí.</span><span class="sxs-lookup"><span data-stu-id="7b446-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="7b446-136">Tady je definice rozhraní:</span><span class="sxs-lookup"><span data-stu-id="7b446-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="7b446-137">**IDependencyScope** rozhraní má dvě metody:</span><span class="sxs-lookup"><span data-stu-id="7b446-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="7b446-138">**GetService** vytvoří jednu instanci typu.</span><span class="sxs-lookup"><span data-stu-id="7b446-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="7b446-139">**GetServices** vytvoří kolekci objektů zadaného typu.</span><span class="sxs-lookup"><span data-stu-id="7b446-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="7b446-140">**IDependencyResolver** dědí metodu **IDependencyScope** a přidá **BeginScope** metody.</span><span class="sxs-lookup"><span data-stu-id="7b446-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="7b446-141">O oborech můžu zabývat později v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="7b446-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="7b446-142">Pokud webové rozhraní API vytvoří instanci kontroleru, nejprve volá **IDependencyResolver.GetService**, předejte typ kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7b446-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="7b446-143">Toto rozšíření zavěšení můžete použít k vytvoření kontroleru, řešení případných závislostí.</span><span class="sxs-lookup"><span data-stu-id="7b446-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="7b446-144">Pokud **GetService** , vrátí hodnotu null, vyhledá webového rozhraní API pro konstruktor třídy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7b446-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="7b446-145">Řešení závislostí s kontejnerem Unity</span><span class="sxs-lookup"><span data-stu-id="7b446-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="7b446-146">I když můžete napsat kompletní **IDependencyResolver** implementace úplně od začátku, rozhraní je ve skutečnosti navrženy tak, aby fungoval jako most mezi webovým rozhraním API a existující kontejnery IoC.</span><span class="sxs-lookup"><span data-stu-id="7b446-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="7b446-147">Kontejner IoC je softwarová součást, která zodpovídá za správu závislostí.</span><span class="sxs-lookup"><span data-stu-id="7b446-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="7b446-148">Registrace typů s kontejnerem a následné použití k vytvoření objektů kontejneru.</span><span class="sxs-lookup"><span data-stu-id="7b446-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="7b446-149">Kontejner automaticky zjistí vztahy závislostí.</span><span class="sxs-lookup"><span data-stu-id="7b446-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="7b446-150">Spousta kontejnerů IoC také umožňují řídit věci, jako je životní cyklus objektů a obor.</span><span class="sxs-lookup"><span data-stu-id="7b446-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="7b446-151">"IoC" znamená "inverzi ovládacího prvku", což je obecný vzor, pokud rámec volání do kódu aplikace.</span><span class="sxs-lookup"><span data-stu-id="7b446-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="7b446-152">Kontejner IoC vytvoří objekty, které "Invertuje" obvyklý tok řízení.</span><span class="sxs-lookup"><span data-stu-id="7b446-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="7b446-153">V tomto kurzu použijeme [Unity](https://msdn.microsoft.com/library/ff647202.aspx) z Microsoft Patterns &amp; postupy.</span><span class="sxs-lookup"><span data-stu-id="7b446-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="7b446-154">(Zahrnout další oblíbené knihovny [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), a [StructureMap ](http://structuremap.github.io/documentation/).) Správce balíčků NuGet můžete nainstalovat Unity.</span><span class="sxs-lookup"><span data-stu-id="7b446-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="7b446-155">Z **nástroje** v aplikaci Visual Studio, vyberte v nabídce **Správce balíčků NuGet**, vyberte **konzoly Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="7b446-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7b446-156">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="7b446-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="7b446-157">Tady je implementace **IDependencyResolver** tím končí naše kontejner Unity.</span><span class="sxs-lookup"><span data-stu-id="7b446-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="7b446-158">Pokud **GetService** metodu nelze přeložit typ, měla by vrátit **null**.</span><span class="sxs-lookup"><span data-stu-id="7b446-158">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="7b446-159">Pokud **GetServices** metodu nelze přeložit typ, měla by vrátit objekt prázdnou kolekci.</span><span class="sxs-lookup"><span data-stu-id="7b446-159">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="7b446-160">Není vyvolávat výjimky pro neznámé typy.</span><span class="sxs-lookup"><span data-stu-id="7b446-160">Don't throw exceptions for unknown types.</span></span>

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="7b446-161">Konfigurace překladač závislostí</span><span class="sxs-lookup"><span data-stu-id="7b446-161">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="7b446-162">Nastavit překladače závislostí **překladače závislostí** vlastnost globálního **HttpConfiguration** objektu.</span><span class="sxs-lookup"><span data-stu-id="7b446-162">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="7b446-163">Následující kód registrů `IProductRepository` rozhraní pomocí Unity a pak vytvoří `UnityResolver`.</span><span class="sxs-lookup"><span data-stu-id="7b446-163">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="7b446-164">Závislost oboru a životnosti Kontroleru</span><span class="sxs-lookup"><span data-stu-id="7b446-164">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="7b446-165">Kontrolery se vytvoří každý požadavek.</span><span class="sxs-lookup"><span data-stu-id="7b446-165">Controllers are created per request.</span></span> <span data-ttu-id="7b446-166">Ke správě životnosti objektu **IDependencyResolver** používá koncept *oboru*.</span><span class="sxs-lookup"><span data-stu-id="7b446-166">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="7b446-167">Překladač závislostí, který je připojen k **HttpConfiguration** objektu má globální obor.</span><span class="sxs-lookup"><span data-stu-id="7b446-167">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="7b446-168">Webové rozhraní API vytvoří kontroler, volá **BeginScope**.</span><span class="sxs-lookup"><span data-stu-id="7b446-168">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="7b446-169">Tato metoda vrátí **IDependencyScope** , která představuje podřízeném oboru.</span><span class="sxs-lookup"><span data-stu-id="7b446-169">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="7b446-170">Potom volá webové rozhraní API **GetService** v podřízeném oboru pro vytvoření kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7b446-170">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="7b446-171">Po dokončení žádosti se volá webové rozhraní API **Dispose** v podřízeném oboru.</span><span class="sxs-lookup"><span data-stu-id="7b446-171">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="7b446-172">Použití **Dispose** metodu dispose závislostí kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7b446-172">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="7b446-173">Jak implementovat **BeginScope** závisí na kontejner IoC.</span><span class="sxs-lookup"><span data-stu-id="7b446-173">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="7b446-174">Pro Unity odpovídá rozsahu podřízený kontejner:</span><span class="sxs-lookup"><span data-stu-id="7b446-174">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="7b446-175">Většina IoC kontejnery mají podobné ekvivalenty.</span><span class="sxs-lookup"><span data-stu-id="7b446-175">Most IoC containers have similar equivalents.</span></span>
