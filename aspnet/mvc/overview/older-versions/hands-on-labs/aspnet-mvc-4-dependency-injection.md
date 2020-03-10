---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: Vkládání závislostí ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 'Poznámka: Tato praktická cvičení předpokládá, že máte základní znalosti o ASP.NET MVC a ASP.NETch filtrech MVC 4. Pokud jste předtím nepoužívali ASP.NET filtry MVC 4, připravujeme...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560611"
---
# <a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="8289f-104">ASP.NET MVC 4 – injektáž závislostí</span><span class="sxs-lookup"><span data-stu-id="8289f-104">ASP.NET MVC 4 Dependency Injection</span></span>

<span data-ttu-id="8289f-105">podle [týmu webového Campy](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="8289f-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="8289f-106">Stáhnout web Campy Training Kit</span><span class="sxs-lookup"><span data-stu-id="8289f-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="8289f-107">Tato praktická cvičení předpokládá, že máte základní znalosti o filtrech **ASP.NET MVC** a **ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="8289f-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="8289f-108">Pokud jste předtím nepoužívali **ASP.NET filtry MVC 4** , doporučujeme, abyste si převzali více než v praxi **vlastní filtry akcí ASP.NET MVC** .</span><span class="sxs-lookup"><span data-stu-id="8289f-108">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="8289f-109">Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Training Kit, která je dostupná v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="8289f-109">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="8289f-110">Projekt, který je specifický pro toto testovací prostředí, je k dispozici pro [vkládání závislostí ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span><span class="sxs-lookup"><span data-stu-id="8289f-110">The project specific to this lab is available at [ASP.NET MVC 4 Dependency Injection](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span></span>

<span data-ttu-id="8289f-111">V **objektově orientovaném programovacím** paradigmatu objekty spolupracují v modelu spolupráce, kde jsou přispěvatelé a příjemci.</span><span class="sxs-lookup"><span data-stu-id="8289f-111">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="8289f-112">Přirozeně tento komunikační model generuje závislosti mezi objekty a komponentami a je obtížné ho spravovat, když se zvyšuje složitost.</span><span class="sxs-lookup"><span data-stu-id="8289f-112">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="8289f-113">![Závislosti tříd a složitost modelu](aspnet-mvc-4-dependency-injection/_static/image1.png "Závislosti tříd a složitost modelu")</span><span class="sxs-lookup"><span data-stu-id="8289f-113">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="8289f-114">*Závislosti tříd a složitost modelu*</span><span class="sxs-lookup"><span data-stu-id="8289f-114">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="8289f-115">Pravděpodobně jste se dozvěděli o **modelu továrny** a oddělení mezi rozhraním a implementací pomocí služeb, kde jsou objekty klienta často zodpovědné za umístění služby.</span><span class="sxs-lookup"><span data-stu-id="8289f-115">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="8289f-116">Vzor injektáže závislosti je konkrétní implementace inverze ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="8289f-116">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="8289f-117">**Inverze ovládacího prvku (IOC)** znamená, že objekty nevytvářejí další objekty, na kterých spoléhají na jejich práci.</span><span class="sxs-lookup"><span data-stu-id="8289f-117">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="8289f-118">Místo toho získají objekty, které potřebují z vnějšího zdroje (například konfigurační soubor XML).</span><span class="sxs-lookup"><span data-stu-id="8289f-118">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="8289f-119">**Vkládání závislostí (di)** znamená, že je provedeno bez zásahu objektu, obvykle komponentou rozhraní, která předá parametry konstruktoru a nastavují vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="8289f-119">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="8289f-120">Vzor návrhu vkládání závislostí (DI)</span><span class="sxs-lookup"><span data-stu-id="8289f-120">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="8289f-121">V nejvyšší úrovni je cílem injektáže závislostí, že třída klienta (například *Golf*) potřebuje něco, co splňuje rozhraní (např. *IClub*).</span><span class="sxs-lookup"><span data-stu-id="8289f-121">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="8289f-122">Nezáleží na tom, jaký konkrétní typ je (např. *WoodClub, IronClub, WedgeClub* nebo *PutterClub*), chce někomu jinému, aby to zpracovával (například dobrý *Caddy*).</span><span class="sxs-lookup"><span data-stu-id="8289f-122">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="8289f-123">Překladač závislostí v ASP.NET MVC vám může dovolit zaregistrovat logiku závislosti někde jinde (například kontejner nebo *penalto*).</span><span class="sxs-lookup"><span data-stu-id="8289f-123">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="8289f-124">![Diagram injektáže závislosti](aspnet-mvc-4-dependency-injection/_static/image2.png "Ilustrace injektáže závislosti")</span><span class="sxs-lookup"><span data-stu-id="8289f-124">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="8289f-125">*Vložení závislostí – Analogová a golfová*</span><span class="sxs-lookup"><span data-stu-id="8289f-125">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="8289f-126">Výhody použití vzoru injektáže závislosti a inverze ovládacího prvku jsou následující:</span><span class="sxs-lookup"><span data-stu-id="8289f-126">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="8289f-127">Zmenší párování tříd.</span><span class="sxs-lookup"><span data-stu-id="8289f-127">Reduces class coupling</span></span>
- <span data-ttu-id="8289f-128">Zvyšuje znovu použití kódu.</span><span class="sxs-lookup"><span data-stu-id="8289f-128">Increases code reusing</span></span>
- <span data-ttu-id="8289f-129">Vylepšuje udržovatelnost kódu</span><span class="sxs-lookup"><span data-stu-id="8289f-129">Improves code maintainability</span></span>
- <span data-ttu-id="8289f-130">Vylepšuje testování aplikací</span><span class="sxs-lookup"><span data-stu-id="8289f-130">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="8289f-131">Vkládání závislostí se někdy porovnává s abstraktním vzorem návrhu výroby, ale mezi oběma přístupy je mírně rozdíl.</span><span class="sxs-lookup"><span data-stu-id="8289f-131">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="8289f-132">DI má architekturu pro řešení závislostí voláním továrn a registrovaných služeb.</span><span class="sxs-lookup"><span data-stu-id="8289f-132">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>

<span data-ttu-id="8289f-133">Teď, když rozumíte vzoru vkládání závislostí, se v tomto testovacím prostředí naučíte, jak ho použít v ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="8289f-133">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="8289f-134">Zahájíte použití injektáže závislosti v **řadičích** pro zahrnutí služby přístupu k databázi.</span><span class="sxs-lookup"><span data-stu-id="8289f-134">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="8289f-135">V dalším kroku použijete vložení závislostí na **zobrazení** , která budou využívat službu a zobrazí informace.</span><span class="sxs-lookup"><span data-stu-id="8289f-135">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="8289f-136">Nakonec rozšíříte filtry DI na ASP.NET MVC 4 a vložíte do řešení vlastní filtr akcí.</span><span class="sxs-lookup"><span data-stu-id="8289f-136">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="8289f-137">V této praktické laboratorní laboratoři se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="8289f-137">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="8289f-138">Integrace ASP.NET MVC 4 s Unity pro vkládání závislostí pomocí balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="8289f-138">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="8289f-139">Použití injektáže závislosti v rámci kontroleru ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="8289f-139">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="8289f-140">Použití injektáže závislosti v zobrazení ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="8289f-140">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="8289f-141">Použití injektáže závislosti v rámci filtru akcí ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="8289f-141">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="8289f-142">Toto testovací prostředí používá balíček NuGet. Mvc3 pro řešení závislostí, ale je možné přizpůsobit libovolné rozhraní injektáže závislostí pro práci s ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="8289f-142">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="8289f-143">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="8289f-143">Prerequisites</span></span>

<span data-ttu-id="8289f-144">K dokončení tohoto testovacího prostředí musíte mít následující položky:</span><span class="sxs-lookup"><span data-stu-id="8289f-144">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="8289f-145">[Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).</span><span class="sxs-lookup"><span data-stu-id="8289f-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="8289f-146">Nastavení</span><span class="sxs-lookup"><span data-stu-id="8289f-146">Setup</span></span>

<span data-ttu-id="8289f-147">**Instalace fragmentů kódu**</span><span class="sxs-lookup"><span data-stu-id="8289f-147">**Installing Code Snippets**</span></span>

<span data-ttu-id="8289f-148">Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8289f-148">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="8289f-149">Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .</span><span class="sxs-lookup"><span data-stu-id="8289f-149">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="8289f-150">Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze B: použití fragmentů kódu](#AppendixB)&quot;.</span><span class="sxs-lookup"><span data-stu-id="8289f-150">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="8289f-151">Cvičení</span><span class="sxs-lookup"><span data-stu-id="8289f-151">Exercises</span></span>

<span data-ttu-id="8289f-152">Tato praktická cvičení se skládají z následujících cvičení:</span><span class="sxs-lookup"><span data-stu-id="8289f-152">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="8289f-153">Cvičení 1: vložení kontroleru</span><span class="sxs-lookup"><span data-stu-id="8289f-153">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="8289f-154">Cvičení 2: Vložení zobrazení</span><span class="sxs-lookup"><span data-stu-id="8289f-154">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="8289f-155">Cvičení 3: vložení filtrů</span><span class="sxs-lookup"><span data-stu-id="8289f-155">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="8289f-156">Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení.</span><span class="sxs-lookup"><span data-stu-id="8289f-156">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="8289f-157">Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.</span><span class="sxs-lookup"><span data-stu-id="8289f-157">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="8289f-158">Odhadovaný čas dokončení tohoto testovacího prostředí: **30 minut**.</span><span class="sxs-lookup"><span data-stu-id="8289f-158">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="8289f-159">Cvičení 1: vložení kontroleru</span><span class="sxs-lookup"><span data-stu-id="8289f-159">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="8289f-160">V tomto cvičení se naučíte používat vkládání závislostí v řadičích ASP.NET MVC integrací Unity pomocí balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="8289f-160">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="8289f-161">Z tohoto důvodu byste do řadičů MvcMusicStore zahrnuli služby, které budou oddělit logiku od přístupu k datům.</span><span class="sxs-lookup"><span data-stu-id="8289f-161">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="8289f-162">Služby vytvoří novou závislost v konstruktoru kontroleru, který bude vyřešen pomocí injektáže závislostí s využitím **Unity**.</span><span class="sxs-lookup"><span data-stu-id="8289f-162">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="8289f-163">Tento přístup vám ukáže, jak vygenerovat méně propojených aplikací, které jsou flexibilnější a jednodušší při údržbě a testování.</span><span class="sxs-lookup"><span data-stu-id="8289f-163">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="8289f-164">Naučíte se také, jak integrovat ASP.NET MVC s Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-164">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="8289f-165">O službě StoreManager</span><span class="sxs-lookup"><span data-stu-id="8289f-165">About StoreManager Service</span></span>

<span data-ttu-id="8289f-166">Hudební úložiště MVC poskytované v řešení zahájit teď obsahuje službu, která spravuje data kontroleru úložiště s názvem **StoreService**.</span><span class="sxs-lookup"><span data-stu-id="8289f-166">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="8289f-167">Níže najdete implementaci služby Store.</span><span class="sxs-lookup"><span data-stu-id="8289f-167">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="8289f-168">Všimněte si, že všechny metody vrací entity modelu.</span><span class="sxs-lookup"><span data-stu-id="8289f-168">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="8289f-169">**StoreController** z řešení Begin teď spotřebovává **StoreService**.</span><span class="sxs-lookup"><span data-stu-id="8289f-169">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="8289f-170">Všechny odkazy na data se odebraly z **StoreController**a teď je možné změnit stávajícího poskytovatele přístupu k datům, aniž byste museli měnit žádnou metodu, která využívá **StoreService**.</span><span class="sxs-lookup"><span data-stu-id="8289f-170">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="8289f-171">Zjistíte, že implementace **StoreController** má závislost s **StoreService** uvnitř konstruktoru třídy.</span><span class="sxs-lookup"><span data-stu-id="8289f-171">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="8289f-172">Závislost představená v tomto cvičení se vztahuje k **inverze řízení** (IOC).</span><span class="sxs-lookup"><span data-stu-id="8289f-172">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="8289f-173">Konstruktor třídy **StoreController** přijímá parametr typu **IStoreService** , který je nezbytný pro provádění volání služby zevnitř třídy.</span><span class="sxs-lookup"><span data-stu-id="8289f-173">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="8289f-174">**StoreController** však neimplementuje výchozí konstruktor (bez parametrů), že musí mít každý kontroler fungovat s ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="8289f-174">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="8289f-175">Chcete-li vyřešit závislost, musí být kontrolér vytvořen abstraktní továrnou (třída, která vrací libovolný objekt zadaného typu).</span><span class="sxs-lookup"><span data-stu-id="8289f-175">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="8289f-176">Pokud se třída pokusí vytvořit StoreController bez odeslání objektu služby, zobrazí se chyba, protože není deklarován konstruktor bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="8289f-176">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="8289f-177">Úloha 1 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="8289f-177">Task 1 - Running the Application</span></span>

<span data-ttu-id="8289f-178">V této úloze spustíte aplikaci Begin, která bude zahrnovat službu do řadiče úložiště, který odděluje přístup k datům z aplikační logiky.</span><span class="sxs-lookup"><span data-stu-id="8289f-178">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="8289f-179">Při spuštění aplikace se zobrazí výjimka, protože služba kontroleru se ve výchozím nastavení nepředává jako parametr:</span><span class="sxs-lookup"><span data-stu-id="8289f-179">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="8289f-180">Otevřete řešení **začít** umístěné v **Source\Ex01-injecting Controller\Begin**.</span><span class="sxs-lookup"><span data-stu-id="8289f-180">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

   1. <span data-ttu-id="8289f-181">Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="8289f-181">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="8289f-182">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8289f-182">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="8289f-183">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="8289f-183">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="8289f-184">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="8289f-184">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8289f-185">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="8289f-185">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="8289f-186">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="8289f-186">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="8289f-187">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="8289f-187">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="8289f-188">Stisknutím **kombinace kláves CTRL + F5** spusťte aplikaci bez ladění.</span><span class="sxs-lookup"><span data-stu-id="8289f-188">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="8289f-189">Zobrazí se chybová zpráva &quot;**pro tento objekt není definován konstruktor bez parametrů**&quot;:</span><span class="sxs-lookup"><span data-stu-id="8289f-189">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="8289f-190">![Chyba při spouštění aplikace ASP.NET MVC begin](aspnet-mvc-4-dependency-injection/_static/image3.png "Chyba při spouštění aplikace ASP.NET MVC begin")</span><span class="sxs-lookup"><span data-stu-id="8289f-190">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="8289f-191">*Chyba při spouštění aplikace ASP.NET MVC begin*</span><span class="sxs-lookup"><span data-stu-id="8289f-191">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="8289f-192">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="8289f-192">Close the browser.</span></span>

<span data-ttu-id="8289f-193">V následujících krocích budete v řešení úložiště pro hudbu pracovat s cílem vložit závislost, kterou tento kontroler potřebuje.</span><span class="sxs-lookup"><span data-stu-id="8289f-193">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="8289f-194">Úkol 2 – zahrnutí Unity do řešení MvcMusicStore</span><span class="sxs-lookup"><span data-stu-id="8289f-194">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="8289f-195">V této úloze budete do řešení zahrnout balíček NuGet **. Mvc3** NuGet.</span><span class="sxs-lookup"><span data-stu-id="8289f-195">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="8289f-196">Balíček Unity. Mvc3 byl navržen pro ASP.NET MVC 3, ale je plně kompatibilní s ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="8289f-196">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="8289f-197">Unity je jednoduchý a rozšiřitelný kontejner vkládání závislostí s volitelnou podporou pro instance a zachycení typu.</span><span class="sxs-lookup"><span data-stu-id="8289f-197">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="8289f-198">Je to kontejner pro obecné účely pro použití v jakémkoli typu aplikace .NET.</span><span class="sxs-lookup"><span data-stu-id="8289f-198">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="8289f-199">Poskytuje všechny společné funkce v mechanismech injektáže závislostí, včetně: vytvoření objektu, abstrakce požadavků zadáním závislostí za běhu a flexibilitu, odložením konfigurace komponenty do kontejneru.</span><span class="sxs-lookup"><span data-stu-id="8289f-199">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>

1. <span data-ttu-id="8289f-200">Nainstalujte balíček NuGet **. Mvc3** NuGet do projektu **MvcMusicStore** .</span><span class="sxs-lookup"><span data-stu-id="8289f-200">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="8289f-201">Provedete to tak, že otevřete **konzolu Správce balíčků** ze **zobrazení** | **jiných oknech**.</span><span class="sxs-lookup"><span data-stu-id="8289f-201">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="8289f-202">Spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="8289f-202">Run the following command.</span></span>

    <span data-ttu-id="8289f-203">PMC</span><span class="sxs-lookup"><span data-stu-id="8289f-203">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="8289f-204">![Instaluje se balíček NuGet. Mvc3 NuGet.](aspnet-mvc-4-dependency-injection/_static/image4.png "Instaluje se balíček NuGet. Mvc3 NuGet.")</span><span class="sxs-lookup"><span data-stu-id="8289f-204">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="8289f-205">*Instaluje se balíček NuGet. Mvc3 NuGet.*</span><span class="sxs-lookup"><span data-stu-id="8289f-205">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="8289f-206">Jakmile je balíček **Unity. Mvc3** nainstalovaný, prozkoumejte soubory a složky, které automaticky přidá, aby se zjednodušila konfigurace Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-206">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="8289f-207">![Balíček Unity. Mvc3 je nainstalovaný.](aspnet-mvc-4-dependency-injection/_static/image5.png "Balíček Unity. Mvc3 je nainstalovaný.")</span><span class="sxs-lookup"><span data-stu-id="8289f-207">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="8289f-208">*Balíček Unity. Mvc3 je nainstalovaný.*</span><span class="sxs-lookup"><span data-stu-id="8289f-208">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a><span data-ttu-id="8289f-209">Úloha 3 – registrace Unity v Global.asax.cs aplikaci\_Start</span><span class="sxs-lookup"><span data-stu-id="8289f-209">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="8289f-210">V této úloze aktualizujete metodu **\_aplikace** , která se nachází v **Global.asax.cs** , aby volala inicializátor zaváděcího nástroje Unity a pak aktualizovala soubor zaváděcího nástroje, který registruje službu a řadič, který budete používat pro vkládání závislostí.</span><span class="sxs-lookup"><span data-stu-id="8289f-210">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="8289f-211">Teď se připojíte ke zaváděcímu programu, který je souborem, který inicializuje kontejner Unity a překladač závislostí.</span><span class="sxs-lookup"><span data-stu-id="8289f-211">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="8289f-212">Provedete to tak, že otevřete **Global.asax.cs** a do **aplikace\_Start** přidáte následující zvýrazněný kód.</span><span class="sxs-lookup"><span data-stu-id="8289f-212">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="8289f-213">(Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex01-Initialize Unity*)</span><span class="sxs-lookup"><span data-stu-id="8289f-213">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="8289f-214">Otevřete soubor **Bootstrapper.cs** .</span><span class="sxs-lookup"><span data-stu-id="8289f-214">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="8289f-215">Zahrňte následující obory názvů: **MvcMusicStore. Services** a **MusicStore. Controllers**.</span><span class="sxs-lookup"><span data-stu-id="8289f-215">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="8289f-216">(Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex01-zaváděcí obory názvů*)</span><span class="sxs-lookup"><span data-stu-id="8289f-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="8289f-217">Nahraďte obsah metody **BuildUnityContainer** následujícím kódem, který registruje řadič úložiště a službu úložiště.</span><span class="sxs-lookup"><span data-stu-id="8289f-217">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="8289f-218">(Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex01 – registrace kontroleru a služby úložiště*)</span><span class="sxs-lookup"><span data-stu-id="8289f-218">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="8289f-219">Úloha 4 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="8289f-219">Task 4 - Running the Application</span></span>

<span data-ttu-id="8289f-220">V této úloze spustíte aplikaci, abyste ověřili, že se teď dá načíst po zahrnutí Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-220">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="8289f-221">Stisknutím klávesy **F5** spusťte aplikaci, aplikace by se nyní měla načíst bez zobrazení jakékoli chybové zprávy.</span><span class="sxs-lookup"><span data-stu-id="8289f-221">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="8289f-222">![Běžící aplikace se vkládáním závislostí](aspnet-mvc-4-dependency-injection/_static/image6.png "Běžící aplikace se vkládáním závislostí")</span><span class="sxs-lookup"><span data-stu-id="8289f-222">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="8289f-223">*Běžící aplikace se vkládáním závislostí*</span><span class="sxs-lookup"><span data-stu-id="8289f-223">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="8289f-224">Přejděte na **/Store**.</span><span class="sxs-lookup"><span data-stu-id="8289f-224">Browse to **/Store**.</span></span> <span data-ttu-id="8289f-225">Tím se vyvolá **StoreController**, který se teď vytvoří pomocí **Unity**.</span><span class="sxs-lookup"><span data-stu-id="8289f-225">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="8289f-226">![Hudební úložiště MVC](aspnet-mvc-4-dependency-injection/_static/image7.png "Hudební úložiště MVC")</span><span class="sxs-lookup"><span data-stu-id="8289f-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="8289f-227">*Hudební úložiště MVC*</span><span class="sxs-lookup"><span data-stu-id="8289f-227">*MVC Music Store*</span></span>
3. <span data-ttu-id="8289f-228">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="8289f-228">Close the browser.</span></span>

<span data-ttu-id="8289f-229">V následujících cvičeních se naučíte, jak rozšířením oboru pro vkládání závislostí použít uvnitř zobrazení ASP.NET MVC a filtry akcí.</span><span class="sxs-lookup"><span data-stu-id="8289f-229">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="8289f-230">Cvičení 2: Vložení zobrazení</span><span class="sxs-lookup"><span data-stu-id="8289f-230">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="8289f-231">V tomto cvičení se naučíte používat vkládání závislostí v zobrazení s novými funkcemi ASP.NET MVC 4 pro integraci Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-231">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="8289f-232">Aby to bylo možné, budete volat vlastní službu v zobrazení pro procházení úložiště, ve kterém se zobrazí zpráva a obrázek níže.</span><span class="sxs-lookup"><span data-stu-id="8289f-232">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="8289f-233">Pak budete projekt integrovat s Unity a vytvoříte vlastní překladač závislostí pro vložení závislostí.</span><span class="sxs-lookup"><span data-stu-id="8289f-233">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="8289f-234">Úkol 1 – Vytvoření zobrazení, které využívá službu</span><span class="sxs-lookup"><span data-stu-id="8289f-234">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="8289f-235">V této úloze vytvoříte zobrazení, které provede volání služby, aby se vygenerovala nová závislost.</span><span class="sxs-lookup"><span data-stu-id="8289f-235">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="8289f-236">Služba se skládá z jednoduché služby zasílání zpráv zahrnuté v tomto řešení.</span><span class="sxs-lookup"><span data-stu-id="8289f-236">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="8289f-237">Otevřete řešení **začít** umístěné ve složce **Source\Ex02-injecting View\Begin** .</span><span class="sxs-lookup"><span data-stu-id="8289f-237">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="8289f-238">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="8289f-238">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="8289f-239">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="8289f-239">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="8289f-240">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8289f-240">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="8289f-241">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="8289f-241">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="8289f-242">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="8289f-242">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8289f-243">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="8289f-243">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="8289f-244">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="8289f-244">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="8289f-245">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="8289f-245">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="8289f-246">Další informace najdete v tomto článku: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="8289f-246">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="8289f-247">Zahrňte třídy **MessageService.cs** a **IMessageService.cs** umístěné ve složce **source \Assets** v **/Services**.</span><span class="sxs-lookup"><span data-stu-id="8289f-247">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="8289f-248">Provedete to tak, že kliknete pravým tlačítkem na složku **služby** a vyberete **Přidat existující položku**.</span><span class="sxs-lookup"><span data-stu-id="8289f-248">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="8289f-249">Vyhledejte umístění soubory a zahrňte je.</span><span class="sxs-lookup"><span data-stu-id="8289f-249">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="8289f-250">![Přidání služby zpráv a rozhraní služby](aspnet-mvc-4-dependency-injection/_static/image8.png "Přidání služby zpráv a rozhraní služby")</span><span class="sxs-lookup"><span data-stu-id="8289f-250">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="8289f-251">*Přidání služby zpráv a rozhraní služby*</span><span class="sxs-lookup"><span data-stu-id="8289f-251">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="8289f-252">Rozhraní **IMessageService** definuje dvě vlastnosti implementované třídou **MessageService** .</span><span class="sxs-lookup"><span data-stu-id="8289f-252">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="8289f-253">Tyto vlastnosti –**zpráva** a **ImageUrl**– uloží zprávu a adresu URL obrázku, který se má zobrazit.</span><span class="sxs-lookup"><span data-stu-id="8289f-253">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="8289f-254">Vytvořte složku **/Pages** v kořenové složce projektu a pak přidejte existující třídu **MyBasePage.cs** z **Source\Assets**.</span><span class="sxs-lookup"><span data-stu-id="8289f-254">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="8289f-255">Základní stránka, ze které budete dědit, má následující strukturu.</span><span class="sxs-lookup"><span data-stu-id="8289f-255">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="8289f-256">![Složka stránky](aspnet-mvc-4-dependency-injection/_static/image9.png "Složka stránky")</span><span class="sxs-lookup"><span data-stu-id="8289f-256">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="8289f-257">Otevřete zobrazení **Procházet. cshtml** ze složky **/views/Store** a nastavte jeho dědění z **MyBasePage.cs**.</span><span class="sxs-lookup"><span data-stu-id="8289f-257">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="8289f-258">V zobrazení **Procházet** přidejte volání **MessageService** k zobrazení obrázku a zprávy, kterou služba získala.</span><span class="sxs-lookup"><span data-stu-id="8289f-258">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
   <span data-ttu-id="8289f-259">(C#)</span><span class="sxs-lookup"><span data-stu-id="8289f-259">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="8289f-260">Úloha 2 – včetně vlastního překladače závislostí a vlastní aktivační procedury stránky zobrazení</span><span class="sxs-lookup"><span data-stu-id="8289f-260">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="8289f-261">V předchozím úkolu jste do zobrazení vložili novou závislost, která v rámci něj provede volání služby.</span><span class="sxs-lookup"><span data-stu-id="8289f-261">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="8289f-262">Nyní tuto závislost vyřeší implementací rozhraní injektáže závislosti ASP.NET MVC **IViewPageActivator** a **IDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="8289f-262">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="8289f-263">Do řešení zahrnete implementaci **IDependencyResolver** , která se bude zabývat s načítáním služby pomocí Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-263">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="8289f-264">Pak budete zahrnovat další vlastní implementaci rozhraní **IViewPageActivator** , která vyřeší vytváření zobrazení.</span><span class="sxs-lookup"><span data-stu-id="8289f-264">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="8289f-265">Vzhledem k tomu, že ASP.NET MVC 3, implementace pro vkládání závislostí zjednodušila rozhraní k registraci služeb.</span><span class="sxs-lookup"><span data-stu-id="8289f-265">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="8289f-266">**IDependencyResolver** a **IViewPageActivator** jsou součástí funkcí ASP.NET MVC 3 pro vkládání závislostí.</span><span class="sxs-lookup"><span data-stu-id="8289f-266">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="8289f-267">**– Rozhraní IDependencyResolver** nahrazuje předchozí IMvcServiceLocator.</span><span class="sxs-lookup"><span data-stu-id="8289f-267">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="8289f-268">Implementátori třídy IDependencyResolver musí vracet instanci služby nebo kolekce služeb.</span><span class="sxs-lookup"><span data-stu-id="8289f-268">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="8289f-269">**-IViewPageActivator** rozhraní poskytuje podrobnější kontrolu nad tím, jak jsou stránky zobrazení vytvořeny pomocí injektáže závislostí.</span><span class="sxs-lookup"><span data-stu-id="8289f-269">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="8289f-270">Třídy, které implementují rozhraní **IViewPageActivator** , mohou vytvářet instance zobrazení pomocí informací o kontextu.</span><span class="sxs-lookup"><span data-stu-id="8289f-270">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. <span data-ttu-id="8289f-271">Vytvořte složku/**továrny** v kořenové složce projektu.</span><span class="sxs-lookup"><span data-stu-id="8289f-271">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="8289f-272">Zahrňte do svého řešení **CustomViewPageActivator.cs** ze složky **/sources/assets/** to **Factory** .</span><span class="sxs-lookup"><span data-stu-id="8289f-272">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="8289f-273">Provedete to tak, že kliknete pravým tlačítkem na složku **/Factories** , vyberete **Přidat | Existující položka** a pak vyberte **CustomViewPageActivator.cs**.</span><span class="sxs-lookup"><span data-stu-id="8289f-273">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="8289f-274">Tato třída implementuje rozhraní **IViewPageActivator** pro uchování kontejneru Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-274">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="8289f-275">**CustomViewPageActivator** zodpovídá za správu vytváření zobrazení pomocí kontejneru Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-275">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="8289f-276">Zahrnout soubor **UnityDependencyResolver.cs** z **/sources/assets** do složky **/Factories**</span><span class="sxs-lookup"><span data-stu-id="8289f-276">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="8289f-277">Provedete to tak, že kliknete pravým tlačítkem na složku **/Factories** , vyberete **Přidat | Existující položka** a potom vyberte soubor **UnityDependencyResolver.cs** .</span><span class="sxs-lookup"><span data-stu-id="8289f-277">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="8289f-278">Třída **UnityDependencyResolver** je vlastní DependencyResolver pro Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-278">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="8289f-279">Pokud se služba v kontejneru Unity nedá najít, je základní překladač invocated.</span><span class="sxs-lookup"><span data-stu-id="8289f-279">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="8289f-280">V následujících úlohách budou registrovány obě implementace, aby model věděl umístění služeb a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="8289f-280">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="8289f-281">Úloha 3 – registrace pro vkládání závislostí v kontejneru Unity</span><span class="sxs-lookup"><span data-stu-id="8289f-281">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="8289f-282">V této úloze vložíte všechny předchozí věci, aby se provedla práce injektáže.</span><span class="sxs-lookup"><span data-stu-id="8289f-282">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="8289f-283">Až teď vaše řešení obsahuje následující prvky:</span><span class="sxs-lookup"><span data-stu-id="8289f-283">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="8289f-284">Zobrazení **procházení** , které dědí z **MyBaseClass** a spotřebovává **MessageService**.</span><span class="sxs-lookup"><span data-stu-id="8289f-284">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="8289f-285">Zprostředkující třída –**MyBaseClass**– obsahuje vkládání závislostí deklarované pro rozhraní služby.</span><span class="sxs-lookup"><span data-stu-id="8289f-285">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="8289f-286">Služba- **MessageService** -a jeho rozhraní **IMessageService**.</span><span class="sxs-lookup"><span data-stu-id="8289f-286">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="8289f-287">Vlastní překladač závislostí pro Unity- **UnityDependencyResolver** – který se zabývá načítáním služeb.</span><span class="sxs-lookup"><span data-stu-id="8289f-287">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="8289f-288">Stránka zobrazení Activator – **CustomViewPageActivator** – vytvoří stránku.</span><span class="sxs-lookup"><span data-stu-id="8289f-288">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="8289f-289">Pro vložení zobrazení pro **procházení** teď zaregistrujete vlastní překladač závislostí do kontejneru Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-289">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="8289f-290">Otevřete soubor **Bootstrapper.cs** .</span><span class="sxs-lookup"><span data-stu-id="8289f-290">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="8289f-291">Zaregistrujte instanci **MessageService** do kontejneru Unity pro inicializaci služby:</span><span class="sxs-lookup"><span data-stu-id="8289f-291">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="8289f-292">(Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex02-Register Message Service*)</span><span class="sxs-lookup"><span data-stu-id="8289f-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="8289f-293">Přidejte odkaz na obor názvů **MvcMusicStore. Factory** .</span><span class="sxs-lookup"><span data-stu-id="8289f-293">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="8289f-294">(Fragment kódu – *ASP.NET pro vkládání závislostí – obor názvů Ex02-Factory*)</span><span class="sxs-lookup"><span data-stu-id="8289f-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="8289f-295">Zaregistrujte **CustomViewPageActivator** jako aktivátor stránky zobrazení do kontejneru Unity:</span><span class="sxs-lookup"><span data-stu-id="8289f-295">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="8289f-296">(Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex02-Register CustomViewPageActivator*)</span><span class="sxs-lookup"><span data-stu-id="8289f-296">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="8289f-297">Nahraďte výchozí překladač závislostí ASP.NET MVC 4 instancí **UnityDependencyResolver**.</span><span class="sxs-lookup"><span data-stu-id="8289f-297">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="8289f-298">Chcete-li to provést, nahraďte obsah metody **Initialize** následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="8289f-298">To do this, replace **Initialize** method content with the following code:</span></span>

    <span data-ttu-id="8289f-299">(Fragment kódu – *testovací prostředí pro vkládání závislostí ASP.NET – Ex02 – aktualizace překladače závislostí*)</span><span class="sxs-lookup"><span data-stu-id="8289f-299">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="8289f-300">ASP.NET MVC poskytuje výchozí třídu překladače závislosti.</span><span class="sxs-lookup"><span data-stu-id="8289f-300">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="8289f-301">Pokud chcete pracovat s vlastními Překladači závislostí, jako je ta, kterou jsme vytvořili pro Unity, je nutné tento překladač vyměnit.</span><span class="sxs-lookup"><span data-stu-id="8289f-301">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="8289f-302">Úloha 4 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="8289f-302">Task 4 - Running the Application</span></span>

<span data-ttu-id="8289f-303">V této úloze spustíte aplikaci, abyste ověřili, že prohlížeč Store používá službu, a zobrazí se obrázek a načtená zpráva:</span><span class="sxs-lookup"><span data-stu-id="8289f-303">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="8289f-304">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="8289f-304">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="8289f-305">V nabídce žánry klikněte na **rock (Rock** ) a podívejte se, jak byl **MessageService** vložen do zobrazení a načtena uvítací zpráva a obrázek.</span><span class="sxs-lookup"><span data-stu-id="8289f-305">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="8289f-306">V tomto příkladu se zadáváme &quot;**Rock**&quot;:</span><span class="sxs-lookup"><span data-stu-id="8289f-306">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="8289f-307">![Úložiště hudby pro MVC – zobrazení injektáže](aspnet-mvc-4-dependency-injection/_static/image10.png "Úložiště hudby pro MVC – zobrazení injektáže")</span><span class="sxs-lookup"><span data-stu-id="8289f-307">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="8289f-308">*Úložiště hudby pro MVC – zobrazení injektáže*</span><span class="sxs-lookup"><span data-stu-id="8289f-308">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="8289f-309">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="8289f-309">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="8289f-310">Cvičení 3: vkládání filtrů akcí</span><span class="sxs-lookup"><span data-stu-id="8289f-310">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="8289f-311">V předchozích **filtrech vlastních akcí** testovacího prostředí jste pracovali s přizpůsobením a vkládáním filtrů.</span><span class="sxs-lookup"><span data-stu-id="8289f-311">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="8289f-312">V tomto cvičení se naučíte, jak vložit filtry pomocí injektáže závislosti pomocí kontejneru Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-312">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="8289f-313">Chcete-li to provést, přidejte do řešení úložiště hudby vlastní filtr akcí, který bude trasovat aktivitu tohoto webu.</span><span class="sxs-lookup"><span data-stu-id="8289f-313">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="8289f-314">Úkol 1 – včetně sledovacího filtru v řešení</span><span class="sxs-lookup"><span data-stu-id="8289f-314">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="8289f-315">V této úloze zahrnete do úložiště hudby vlastní filtr akcí, ve kterém se budou trasovat události.</span><span class="sxs-lookup"><span data-stu-id="8289f-315">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="8289f-316">Vzhledem k tomu, že koncepty filtru vlastních akcí jsou již ošetřeny v předchozí laboratoři &quot;filtry vlastních akcí&quot;, do složky assets tohoto testovacího prostředí zahrnete pouze třídu Filter a pak vytvoříte zprostředkovatele filtru pro Unity:</span><span class="sxs-lookup"><span data-stu-id="8289f-316">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="8289f-317">Otevřete řešení **zahájit** ve složce **Filter\Begin akce Source\Ex03-vložení** .</span><span class="sxs-lookup"><span data-stu-id="8289f-317">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="8289f-318">V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.</span><span class="sxs-lookup"><span data-stu-id="8289f-318">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="8289f-319">Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="8289f-319">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="8289f-320">Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8289f-320">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="8289f-321">V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="8289f-321">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="8289f-322">Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="8289f-322">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8289f-323">Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu.</span><span class="sxs-lookup"><span data-stu-id="8289f-323">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="8289f-324">Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny.</span><span class="sxs-lookup"><span data-stu-id="8289f-324">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="8289f-325">To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="8289f-325">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="8289f-326">Další informace najdete v tomto článku: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span><span class="sxs-lookup"><span data-stu-id="8289f-326">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="8289f-327">Zahrnout soubor **TraceActionFilter.cs** z **/sources/assets** do složky **/Filters**</span><span class="sxs-lookup"><span data-stu-id="8289f-327">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="8289f-328">Tento vlastní filtr akcí provádí trasování ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8289f-328">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="8289f-329">Další informace najdete v &quot;ASP.NET na základě místní a dynamické filtry akcí MVC 4&quot; Lab.</span><span class="sxs-lookup"><span data-stu-id="8289f-329">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="8289f-330">Přidejte do projektu prázdnou třídu **FilterProvider.cs** ve složce **/filters.**</span><span class="sxs-lookup"><span data-stu-id="8289f-330">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="8289f-331">Přidejte obory názvů **System. Web. Mvc** a **Microsoft. Practices. Unity** v **FilterProvider.cs**.</span><span class="sxs-lookup"><span data-stu-id="8289f-331">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="8289f-332">(Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex03-Filter Provider přidává obory názvů*)</span><span class="sxs-lookup"><span data-stu-id="8289f-332">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="8289f-333">Nastavte třídu na dědění z rozhraní **IFilterProvider** .</span><span class="sxs-lookup"><span data-stu-id="8289f-333">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="8289f-334">Přidejte vlastnost **IUnityContainer** do třídy **FilterProvider** a pak vytvořte konstruktor třídy pro přiřazení kontejneru.</span><span class="sxs-lookup"><span data-stu-id="8289f-334">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="8289f-335">(Fragment kódu – *ASP.NET Dependency injektáže Labs – konstruktor zprostředkovatele filtru Ex03*)</span><span class="sxs-lookup"><span data-stu-id="8289f-335">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="8289f-336">Konstruktor třídy poskytovatele filtru nevytváří **Nový** objekt uvnitř.</span><span class="sxs-lookup"><span data-stu-id="8289f-336">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="8289f-337">Kontejner je předán jako parametr a závislost je vyřešena pomocí Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-337">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="8289f-338">Ve třídě **FilterProvider** Implementujte metody **GetFilters** z rozhraní **IFilterProvider** .</span><span class="sxs-lookup"><span data-stu-id="8289f-338">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="8289f-339">(Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex03-Filter Provider GetFilters*)</span><span class="sxs-lookup"><span data-stu-id="8289f-339">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="8289f-340">Úloha 2 – registrace a povolení filtru</span><span class="sxs-lookup"><span data-stu-id="8289f-340">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="8289f-341">V této úloze povolíte sledování lokality.</span><span class="sxs-lookup"><span data-stu-id="8289f-341">In this task, you will enable site tracking.</span></span> <span data-ttu-id="8289f-342">K tomu je třeba pro spuštění trasování zaregistrovat filtr v metodě **Bootstrapper.cs BuildUnityContainer** :</span><span class="sxs-lookup"><span data-stu-id="8289f-342">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="8289f-343">Otevřete soubor **Web. config** umístěný v kořenovém adresáři projektu a povolte sledování trasování v System. Web Group.</span><span class="sxs-lookup"><span data-stu-id="8289f-343">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="8289f-344">Otevřete **Bootstrapper.cs** v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="8289f-344">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="8289f-345">Přidejte odkaz na obor názvů **MvcMusicStore. filters** .</span><span class="sxs-lookup"><span data-stu-id="8289f-345">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="8289f-346">(Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex03-zaváděcí obory názvů*)</span><span class="sxs-lookup"><span data-stu-id="8289f-346">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="8289f-347">Vyberte metodu **BuildUnityContainer** a zaregistrujte filtr v kontejneru Unity.</span><span class="sxs-lookup"><span data-stu-id="8289f-347">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="8289f-348">Budete muset zaregistrovat poskytovatele filtru i filtr akcí.</span><span class="sxs-lookup"><span data-stu-id="8289f-348">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="8289f-349">(Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex03-Register FilterProvider and ActionFilter*)</span><span class="sxs-lookup"><span data-stu-id="8289f-349">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="8289f-350">Úloha 3 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="8289f-350">Task 3 - Running the Application</span></span>

<span data-ttu-id="8289f-351">V této úloze spustíte aplikaci a otestujete, že filtr vlastní akce trasování aktivity:</span><span class="sxs-lookup"><span data-stu-id="8289f-351">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="8289f-352">Stisknutím klávesy **F5** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="8289f-352">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="8289f-353">V nabídce žánry klikněte na **Rock** .</span><span class="sxs-lookup"><span data-stu-id="8289f-353">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="8289f-354">Pokud chcete, můžete přejít na další žánry.</span><span class="sxs-lookup"><span data-stu-id="8289f-354">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="8289f-355">![Aplikace Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Aplikace Music Store")</span><span class="sxs-lookup"><span data-stu-id="8289f-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="8289f-356">*Aplikace Music Store*</span><span class="sxs-lookup"><span data-stu-id="8289f-356">*Music Store*</span></span>
3. <span data-ttu-id="8289f-357">Přejděte na **/Trace.axd** a zobrazte stránku trasování aplikace a pak klikněte na **Zobrazit podrobnosti**.</span><span class="sxs-lookup"><span data-stu-id="8289f-357">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="8289f-358">![Protokol trasování aplikace](aspnet-mvc-4-dependency-injection/_static/image12.png "Protokol trasování aplikace")</span><span class="sxs-lookup"><span data-stu-id="8289f-358">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="8289f-359">*Protokol trasování aplikace*</span><span class="sxs-lookup"><span data-stu-id="8289f-359">*Application Trace Log*</span></span>

    <span data-ttu-id="8289f-360">![Trasování aplikace – Podrobnosti žádosti](aspnet-mvc-4-dependency-injection/_static/image13.png "Trasování aplikace – Podrobnosti žádosti")</span><span class="sxs-lookup"><span data-stu-id="8289f-360">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="8289f-361">*Trasování aplikace – Podrobnosti žádosti*</span><span class="sxs-lookup"><span data-stu-id="8289f-361">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="8289f-362">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="8289f-362">Close the browser.</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="8289f-363">Souhrn</span><span class="sxs-lookup"><span data-stu-id="8289f-363">Summary</span></span>

<span data-ttu-id="8289f-364">Vyplněním tohoto praktického cvičení jste zjistili, jak používat vkládání závislostí v ASP.NET MVC 4 integrací Unity pomocí balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="8289f-364">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="8289f-365">Pro dosažení tohoto účelu jste použili vkládání závislostí v řadičích, zobrazeních a filtrech akcí.</span><span class="sxs-lookup"><span data-stu-id="8289f-365">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="8289f-366">Byly pokryty následující koncepty:</span><span class="sxs-lookup"><span data-stu-id="8289f-366">The following concepts were covered:</span></span>

- <span data-ttu-id="8289f-367">Funkce injektáže ASP.NET MVC 4 pro vkládání závislostí</span><span class="sxs-lookup"><span data-stu-id="8289f-367">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="8289f-368">Integrace Unity pomocí balíčku NuGet. Mvc3 NuGet</span><span class="sxs-lookup"><span data-stu-id="8289f-368">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="8289f-369">Vkládání závislostí v řadičích</span><span class="sxs-lookup"><span data-stu-id="8289f-369">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="8289f-370">Vkládání závislostí v zobrazeních</span><span class="sxs-lookup"><span data-stu-id="8289f-370">Dependency Injection in Views</span></span>
- <span data-ttu-id="8289f-371">Vložení závislostí filtrů akcí</span><span class="sxs-lookup"><span data-stu-id="8289f-371">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="8289f-372">Příloha A: instalace Visual Studio Express 2012 pro web</span><span class="sxs-lookup"><span data-stu-id="8289f-372">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="8289f-373">**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="8289f-373">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="8289f-374">Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="8289f-374">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="8289f-375">Přejděte do [ (Nastavení)https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) (Integrace a služby).</span><span class="sxs-lookup"><span data-stu-id="8289f-375">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="8289f-376">Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="8289f-376">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="8289f-377">Klikněte na **nainstalovat hned**.</span><span class="sxs-lookup"><span data-stu-id="8289f-377">Click on **Install Now**.</span></span> <span data-ttu-id="8289f-378">Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.</span><span class="sxs-lookup"><span data-stu-id="8289f-378">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="8289f-379">Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.</span><span class="sxs-lookup"><span data-stu-id="8289f-379">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="8289f-380">![Nainstalovat Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="8289f-380">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="8289f-381">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="8289f-381">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="8289f-382">Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**</span><span class="sxs-lookup"><span data-stu-id="8289f-382">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Přijetí licenčních podmínek](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="8289f-384">*Přijetí licenčních podmínek*</span><span class="sxs-lookup"><span data-stu-id="8289f-384">*Accepting the license terms*</span></span>
5. <span data-ttu-id="8289f-385">Počkejte na dokončení procesu stahování a instalace.</span><span class="sxs-lookup"><span data-stu-id="8289f-385">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="8289f-387">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="8289f-387">*Installation progress*</span></span>
6. <span data-ttu-id="8289f-388">Po dokončení instalace klikněte na **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="8289f-388">When the installation completes, click **Finish**.</span></span>

    ![Instalace dokončena](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="8289f-390">*Instalace dokončena*</span><span class="sxs-lookup"><span data-stu-id="8289f-390">*Installation completed*</span></span>
7. <span data-ttu-id="8289f-391">Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="8289f-391">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="8289f-392">Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .</span><span class="sxs-lookup"><span data-stu-id="8289f-392">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![Dlaždice VS Express for Web](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="8289f-394">*Dlaždice VS Express for Web*</span><span class="sxs-lookup"><span data-stu-id="8289f-394">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="8289f-395">Příloha B: použití fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="8289f-395">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="8289f-396">S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="8289f-396">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="8289f-397">Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="8289f-397">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="8289f-398">![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-dependency-injection/_static/image19.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="8289f-398">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="8289f-399">*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*</span><span class="sxs-lookup"><span data-stu-id="8289f-399">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="8289f-400">***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***</span><span class="sxs-lookup"><span data-stu-id="8289f-400">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="8289f-401">Umístěte kurzor na místo, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="8289f-401">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="8289f-402">Začněte psát název fragmentu (bez mezer a spojovníků).</span><span class="sxs-lookup"><span data-stu-id="8289f-402">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="8289f-403">Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.</span><span class="sxs-lookup"><span data-stu-id="8289f-403">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="8289f-404">Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).</span><span class="sxs-lookup"><span data-stu-id="8289f-404">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="8289f-405">Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="8289f-405">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="8289f-406">![Začněte psát název fragmentu.](aspnet-mvc-4-dependency-injection/_static/image20.png "Začněte psát název fragmentu.")</span><span class="sxs-lookup"><span data-stu-id="8289f-406">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="8289f-407">*Začněte psát název fragmentu.*</span><span class="sxs-lookup"><span data-stu-id="8289f-407">*Start typing the snippet name*</span></span>

<span data-ttu-id="8289f-408">![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-dependency-injection/_static/image21.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")</span><span class="sxs-lookup"><span data-stu-id="8289f-408">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="8289f-409">*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*</span><span class="sxs-lookup"><span data-stu-id="8289f-409">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="8289f-410">![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-dependency-injection/_static/image22.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")</span><span class="sxs-lookup"><span data-stu-id="8289f-410">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="8289f-411">*Stiskněte znovu TAB a fragment kódu se rozšíří.*</span><span class="sxs-lookup"><span data-stu-id="8289f-411">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="8289f-412">***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první.</span><span class="sxs-lookup"><span data-stu-id="8289f-412">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="8289f-413">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="8289f-413">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="8289f-414">Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="8289f-414">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="8289f-415">Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="8289f-415">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="8289f-416">![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-dependency-injection/_static/image23.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")</span><span class="sxs-lookup"><span data-stu-id="8289f-416">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="8289f-417">*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*</span><span class="sxs-lookup"><span data-stu-id="8289f-417">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="8289f-418">![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-dependency-injection/_static/image24.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")</span><span class="sxs-lookup"><span data-stu-id="8289f-418">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="8289f-419">*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*</span><span class="sxs-lookup"><span data-stu-id="8289f-419">*Pick the relevant snippet from the list, by clicking on it*</span></span>
