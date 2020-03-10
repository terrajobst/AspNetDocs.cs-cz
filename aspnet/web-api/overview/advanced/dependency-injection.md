---
uid: web-api/overview/advanced/dependency-injection
title: Vkládání závislostí ve webovém rozhraní API ASP.NET 2 – ASP.NET 4. x
author: MikeWasson
description: V tomto kurzu se dozvíte, jak vložit závislosti do kontroleru webového rozhraní API ASP.NET pro ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622603"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="18055-103">Vkládání závislostí ve webovém rozhraní API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="18055-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="18055-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="18055-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="18055-105">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="18055-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="18055-106">V tomto kurzu se dozvíte, jak vložit závislosti do vašeho kontroleru webového rozhraní API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="18055-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="18055-107">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="18055-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="18055-108">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="18055-108">Web API 2</span></span>
> - [<span data-ttu-id="18055-109">Blok aplikace Unity</span><span class="sxs-lookup"><span data-stu-id="18055-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="18055-110">Entity Framework 6 (verze 5 také funguje)</span><span class="sxs-lookup"><span data-stu-id="18055-110">Entity Framework 6 (version 5 also works)</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="18055-111">Co je vkládání závislostí?</span><span class="sxs-lookup"><span data-stu-id="18055-111">What is Dependency Injection?</span></span>

<span data-ttu-id="18055-112">*Závislost* je libovolný objekt, který vyžaduje jiný objekt.</span><span class="sxs-lookup"><span data-stu-id="18055-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="18055-113">Například je běžné definovat [úložiště](http://martinfowler.com/eaaCatalog/repository.html) , které zpracovává přístup k datům.</span><span class="sxs-lookup"><span data-stu-id="18055-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="18055-114">Podívejme se na příklad.</span><span class="sxs-lookup"><span data-stu-id="18055-114">Let's illustrate with an example.</span></span> <span data-ttu-id="18055-115">Nejdřív definujeme model domény:</span><span class="sxs-lookup"><span data-stu-id="18055-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="18055-116">Tady je jednoduchá třída úložiště, která ukládá položky v databázi pomocí Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="18055-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="18055-117">Nyní nadefinujte kontroler webového rozhraní API, který podporuje požadavky GET na `Product` entit.</span><span class="sxs-lookup"><span data-stu-id="18055-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="18055-118">(Jsem opustili POST a další metody pro jednoduchost.) Toto je první pokus:</span><span class="sxs-lookup"><span data-stu-id="18055-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="18055-119">Všimněte si, že třída Controller závisí na `ProductRepository`a my umožňuje řadiči vytvořit instanci `ProductRepository`.</span><span class="sxs-lookup"><span data-stu-id="18055-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="18055-120">To je však špatný nápad, jak tímto způsobem pevně zakódovat závislost, a to z několika důvodů.</span><span class="sxs-lookup"><span data-stu-id="18055-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="18055-121">Pokud chcete nahradit `ProductRepository` jinou implementací, musíte také změnit třídu kontroleru.</span><span class="sxs-lookup"><span data-stu-id="18055-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="18055-122">Pokud `ProductRepository` obsahuje závislosti, musíte je nakonfigurovat v rámci kontroleru.</span><span class="sxs-lookup"><span data-stu-id="18055-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="18055-123">V případě velkého projektu s více řadiči je váš kód konfigurace rozptýlen napříč vaším projektem.</span><span class="sxs-lookup"><span data-stu-id="18055-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="18055-124">Testování částí je obtížné, protože kontroler má pevně zakódovaný dotaz na databázi.</span><span class="sxs-lookup"><span data-stu-id="18055-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="18055-125">Pro testování částí byste měli použít úložiště vzoru nebo zástupné procedury, které není možné s aktuálním návrhem.</span><span class="sxs-lookup"><span data-stu-id="18055-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="18055-126">Tyto problémy můžeme vyřešit *vložením* úložiště do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="18055-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="18055-127">Nejprve refaktorujte třídu `ProductRepository` do rozhraní:</span><span class="sxs-lookup"><span data-stu-id="18055-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="18055-128">Pak zadejte `IProductRepository` jako parametr konstruktoru:</span><span class="sxs-lookup"><span data-stu-id="18055-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="18055-129">Tento příklad používá [vkládání konstruktoru](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="18055-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="18055-130">Lze také použít *Injektáže setter*, kde můžete nastavit závislost prostřednictvím metody setter nebo vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="18055-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="18055-131">Nyní ale dojde k problému, protože aplikace nevytváří kontroler přímo.</span><span class="sxs-lookup"><span data-stu-id="18055-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="18055-132">Webové rozhraní API vytvoří kontroler při směrování žádosti a webové rozhraní API neví o `IProductRepository`žádné informace.</span><span class="sxs-lookup"><span data-stu-id="18055-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="18055-133">Zde je místo, kde se překladač závislostí webového rozhraní API nachází v.</span><span class="sxs-lookup"><span data-stu-id="18055-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="18055-134">Překladač závislostí webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="18055-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="18055-135">Webové rozhraní API definuje rozhraní **IDependencyResolver** pro řešení závislostí.</span><span class="sxs-lookup"><span data-stu-id="18055-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="18055-136">Tady je definice rozhraní:</span><span class="sxs-lookup"><span data-stu-id="18055-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="18055-137">Rozhraní **IDependencyScope** má dvě metody:</span><span class="sxs-lookup"><span data-stu-id="18055-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="18055-138">**GetService** vytvoří jednu instanci typu.</span><span class="sxs-lookup"><span data-stu-id="18055-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="18055-139">**GetService** vytvoří kolekci objektů zadaného typu.</span><span class="sxs-lookup"><span data-stu-id="18055-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="18055-140">Metoda **IDependencyResolver** dědí **IDependencyScope** a přidá metodu **BeginScope** .</span><span class="sxs-lookup"><span data-stu-id="18055-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="18055-141">V tomto kurzu budu mluvit o oborech později.</span><span class="sxs-lookup"><span data-stu-id="18055-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="18055-142">Když webové rozhraní API vytvoří instanci kontroleru, nejprve vyvolá **IDependencyResolver. GetService**, která předává typ kontroleru.</span><span class="sxs-lookup"><span data-stu-id="18055-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="18055-143">Pomocí tohoto zavěšení rozšíření můžete vytvořit kontroler a vyřešit všechny závislosti.</span><span class="sxs-lookup"><span data-stu-id="18055-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="18055-144">Pokud **GetService** vrátí hodnotu null, webové rozhraní API vyhledá konstruktor bez parametrů ve třídě Controller.</span><span class="sxs-lookup"><span data-stu-id="18055-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="18055-145">Řešení závislostí s kontejnerem Unity</span><span class="sxs-lookup"><span data-stu-id="18055-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="18055-146">I když můžete napsat úplnou implementaci **IDependencyResolver** od začátku, rozhraní je ve skutečnosti navržené tak, aby fungovalo jako most mezi WEBOVÝm rozhraním API a stávajícími kontejnery IOC.</span><span class="sxs-lookup"><span data-stu-id="18055-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="18055-147">Kontejner IoC je softwarová součást, která zodpovídá za správu závislostí.</span><span class="sxs-lookup"><span data-stu-id="18055-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="18055-148">Zaregistrujte typy s kontejnerem a potom pomocí kontejneru vytvořte objekty.</span><span class="sxs-lookup"><span data-stu-id="18055-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="18055-149">Kontejner automaticky vyhodnotí vztahy závislostí.</span><span class="sxs-lookup"><span data-stu-id="18055-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="18055-150">Mnoho kontejnerů IoC vám také umožňuje řídit objekty, jako je život a rozsah objektu.</span><span class="sxs-lookup"><span data-stu-id="18055-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="18055-151">"IoC" je zkratka "inverze ovládacího prvku", což je obecný vzor, ve kterém rozhraní volá kód aplikace.</span><span class="sxs-lookup"><span data-stu-id="18055-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="18055-152">Kontejner IoC sestaví vaše objekty za vás, což "Invertuje" běžný tok řízení.</span><span class="sxs-lookup"><span data-stu-id="18055-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>

<span data-ttu-id="18055-153">V tomto kurzu použijeme [Unity](https://msdn.microsoft.com/library/ff647202.aspx) ze vzorů Microsoft patterns &amp; postupů.</span><span class="sxs-lookup"><span data-stu-id="18055-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="18055-154">(Mezi další oblíbené knihovny patří [Castle Windsor](http://www.castleproject.org/), [Spring.NET](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/)a [StructureMap](http://structuremap.github.io/documentation/).) K instalaci Unity můžete použít Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="18055-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="18055-155">V nabídce **nástroje** v aplikaci Visual Studio vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="18055-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="18055-156">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="18055-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="18055-157">Zde je implementace **IDependencyResolver** , která obaluje kontejner Unity.</span><span class="sxs-lookup"><span data-stu-id="18055-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="18055-158">Pokud metoda **GetService** nemůže vyřešit typ, měla by vracet **hodnotu null**.</span><span class="sxs-lookup"><span data-stu-id="18055-158">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="18055-159">Pokud metoda **GetServices** nemůže vyřešit typ, měl by vrátit prázdný objekt kolekce.</span><span class="sxs-lookup"><span data-stu-id="18055-159">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="18055-160">Nevyvolává výjimky pro neznámé typy.</span><span class="sxs-lookup"><span data-stu-id="18055-160">Don't throw exceptions for unknown types.</span></span>

## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="18055-161">Konfigurace překladače závislostí</span><span class="sxs-lookup"><span data-stu-id="18055-161">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="18055-162">Nastavte překladač závislostí na vlastnost **DependencyResolver** globálního objektu **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="18055-162">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="18055-163">Následující kód registruje rozhraní `IProductRepository` s Unity a potom vytvoří `UnityResolver`.</span><span class="sxs-lookup"><span data-stu-id="18055-163">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="18055-164">Obor závislosti a životnost kontroleru</span><span class="sxs-lookup"><span data-stu-id="18055-164">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="18055-165">Řadiče se vytvářejí na základě požadavku.</span><span class="sxs-lookup"><span data-stu-id="18055-165">Controllers are created per request.</span></span> <span data-ttu-id="18055-166">Aby bylo možné spravovat životnost objektů, používá **IDependencyResolver** koncept *oboru*.</span><span class="sxs-lookup"><span data-stu-id="18055-166">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="18055-167">Překladač závislostí připojený k objektu **HttpConfiguration** má globální rozsah.</span><span class="sxs-lookup"><span data-stu-id="18055-167">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="18055-168">Když webové rozhraní API vytvoří kontroler, zavolá **BeginScope**.</span><span class="sxs-lookup"><span data-stu-id="18055-168">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="18055-169">Tato metoda vrací objekt **IDependencyScope** , který představuje podřízený obor.</span><span class="sxs-lookup"><span data-stu-id="18055-169">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="18055-170">Webové rozhraní API pak zavolá metodu **GetService** v podřízeném oboru, aby vytvořila kontroler.</span><span class="sxs-lookup"><span data-stu-id="18055-170">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="18055-171">Po dokončení žádosti webové rozhraní API zavolá **Dispose** v podřízeném oboru.</span><span class="sxs-lookup"><span data-stu-id="18055-171">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="18055-172">K odstranění závislostí řadiče použijte metodu **Dispose** .</span><span class="sxs-lookup"><span data-stu-id="18055-172">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="18055-173">Způsob implementace **BeginScope** závisí na kontejneru IOC.</span><span class="sxs-lookup"><span data-stu-id="18055-173">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="18055-174">V případě Unity rozsah odpovídá podřízenému kontejneru:</span><span class="sxs-lookup"><span data-stu-id="18055-174">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="18055-175">Většina IoCch kontejnerů má podobné ekvivalenty.</span><span class="sxs-lookup"><span data-stu-id="18055-175">Most IoC containers have similar equivalents.</span></span>
