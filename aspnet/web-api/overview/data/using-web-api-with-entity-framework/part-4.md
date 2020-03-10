---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: Zpracování vztahů entit | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557461"
---
# <a name="handling-entity-relations"></a><span data-ttu-id="02f3f-102">Ošetření relací prvků</span><span class="sxs-lookup"><span data-stu-id="02f3f-102">Handling Entity Relations</span></span>

<span data-ttu-id="02f3f-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="02f3f-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="02f3f-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="02f3f-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="02f3f-105">Tato část popisuje některé podrobnosti o tom, jak EF načte související entity, a jak zpracovat cyklické navigační vlastnosti ve třídách modelu.</span><span class="sxs-lookup"><span data-stu-id="02f3f-105">This section describes some details of how EF loads related entities, and how to handle circular navigation properties in your model classes.</span></span> <span data-ttu-id="02f3f-106">(Tato část poskytuje znalosti na pozadí a není nutná k dokončení tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="02f3f-106">(This section provides background knowledge, and is not required to complete the tutorial.</span></span> <span data-ttu-id="02f3f-107">Pokud dáváte přednost, přejděte k [části 5.](part-5.md).)</span><span class="sxs-lookup"><span data-stu-id="02f3f-107">If you prefer, skip to [Part 5.](part-5.md).)</span></span>

## <a name="eager-loading-versus-lazy-loading"></a><span data-ttu-id="02f3f-108">Načítání Eager versus opožděné načítání</span><span class="sxs-lookup"><span data-stu-id="02f3f-108">Eager Loading versus Lazy Loading</span></span>

<span data-ttu-id="02f3f-109">Při použití EF s relační databází je důležité pochopit, jak EF načítají související data.</span><span class="sxs-lookup"><span data-stu-id="02f3f-109">When using EF with a relational database, it's important to understand how EF loads related data.</span></span>

<span data-ttu-id="02f3f-110">Je také užitečné zobrazit dotazy SQL, které EF vygeneruje.</span><span class="sxs-lookup"><span data-stu-id="02f3f-110">It's also useful to see the SQL queries that EF generates.</span></span> <span data-ttu-id="02f3f-111">Chcete-li trasovat SQL, přidejte do konstruktoru `BookServiceContext` následující řádek kódu:</span><span class="sxs-lookup"><span data-stu-id="02f3f-111">To trace the SQL, add the following line of code to the `BookServiceContext` constructor:</span></span>

[!code-csharp[Main](part-4/samples/sample1.cs)]

<span data-ttu-id="02f3f-112">Pokud odešlete požadavek GET na/API/Books, vrátí se JSON podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="02f3f-112">If you send a GET request to /api/books, it returns JSON like the following:</span></span>

[!code-console[Main](part-4/samples/sample2.cmd)]

<span data-ttu-id="02f3f-113">Můžete vidět, že vlastnost Author má hodnotu null, i když kniha obsahuje platný AuthorId.</span><span class="sxs-lookup"><span data-stu-id="02f3f-113">You can see that the Author property is null, even though the book contains a valid AuthorId.</span></span> <span data-ttu-id="02f3f-114">To je proto, že EF nenačítá související entity autora.</span><span class="sxs-lookup"><span data-stu-id="02f3f-114">That's because EF is not loading the related Author entities.</span></span> <span data-ttu-id="02f3f-115">Protokol trasování pro dotaz SQL potvrzuje toto:</span><span class="sxs-lookup"><span data-stu-id="02f3f-115">The trace log of the SQL query confirms this:</span></span>

[!code-console[Main](part-4/samples/sample3.sql)]

<span data-ttu-id="02f3f-116">Příkaz SELECT přijímá z tabulky Books a neodkazuje na tabulku autorů.</span><span class="sxs-lookup"><span data-stu-id="02f3f-116">The SELECT statement takes from the Books table, and does not reference the Author table.</span></span>

<span data-ttu-id="02f3f-117">Pro referenci je zde metoda třídy `BooksController`, která vrací seznam knih.</span><span class="sxs-lookup"><span data-stu-id="02f3f-117">For reference, here is the method in the `BooksController` class that returns the list of books.</span></span>

[!code-csharp[Main](part-4/samples/sample4.cs)]

<span data-ttu-id="02f3f-118">Pojďme se podívat, jak bychom mohli jako součást dat JSON vracet autora.</span><span class="sxs-lookup"><span data-stu-id="02f3f-118">Let's see how we can return the Author as part of the JSON data.</span></span> <span data-ttu-id="02f3f-119">Existují tři způsoby, jak načíst související data v Entity Framework: načítání Eager, opožděné načítání a explicitní načítání.</span><span class="sxs-lookup"><span data-stu-id="02f3f-119">There are three ways to load related data in Entity Framework: eager loading, lazy loading, and explicit loading.</span></span> <span data-ttu-id="02f3f-120">Existují kompromisy s každou technikou, takže je důležité pochopit, jak fungují.</span><span class="sxs-lookup"><span data-stu-id="02f3f-120">There are trade-offs with each technique, so it's important to understand how they work.</span></span>

### <a name="eager-loading"></a><span data-ttu-id="02f3f-121">Eager načítání</span><span class="sxs-lookup"><span data-stu-id="02f3f-121">Eager Loading</span></span>

<span data-ttu-id="02f3f-122">Při *načítání Eager*načítá EF související entity jako součást počátečního databázového dotazu.</span><span class="sxs-lookup"><span data-stu-id="02f3f-122">With *eager loading*, EF loads related entities as part of the initial database query.</span></span> <span data-ttu-id="02f3f-123">K provedení Eager načítání použijte metodu rozšíření **System. data. entity. include** .</span><span class="sxs-lookup"><span data-stu-id="02f3f-123">To perform eager loading, use the **System.Data.Entity.Include** extension method.</span></span>

[!code-csharp[Main](part-4/samples/sample5.cs)]

<span data-ttu-id="02f3f-124">Tato informace oznamuje EF, aby obsahovala data autora v dotazu.</span><span class="sxs-lookup"><span data-stu-id="02f3f-124">This tells EF to include the Author data in the query.</span></span> <span data-ttu-id="02f3f-125">Pokud tuto změnu uděláte a spustíte aplikaci, data JSON teď vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="02f3f-125">If you make this change and run the app, now the JSON data looks like this:</span></span>

[!code-console[Main](part-4/samples/sample6.cmd)]

<span data-ttu-id="02f3f-126">Protokol trasování ukazuje, že EF provedl spojení s knihou a vytvářením tabulek.</span><span class="sxs-lookup"><span data-stu-id="02f3f-126">The trace log shows that EF performed a join on the Book and Author tables.</span></span>

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a><span data-ttu-id="02f3f-127">Opožděné načítání</span><span class="sxs-lookup"><span data-stu-id="02f3f-127">Lazy Loading</span></span>

<span data-ttu-id="02f3f-128">Při opožděném načítání EF automaticky načte související entitu v případě, že je vlastnost navigace pro tuto entitu zpětně odkazovaná.</span><span class="sxs-lookup"><span data-stu-id="02f3f-128">With lazy loading, EF automatically loads a related entity when the navigation property for that entity is dereferenced.</span></span> <span data-ttu-id="02f3f-129">Chcete-li povolit opožděné načítání, nastavte vlastnost navigace jako virtuální.</span><span class="sxs-lookup"><span data-stu-id="02f3f-129">To enable lazy loading, make the navigation property virtual.</span></span> <span data-ttu-id="02f3f-130">Například ve třídě Book:</span><span class="sxs-lookup"><span data-stu-id="02f3f-130">For example, in the Book class:</span></span>

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

<span data-ttu-id="02f3f-131">Nyní zvažte následující kód:</span><span class="sxs-lookup"><span data-stu-id="02f3f-131">Now consider the following code:</span></span>

[!code-csharp[Main](part-4/samples/sample9.cs)]

<span data-ttu-id="02f3f-132">Když je povoleno opožděné načítání, přístup k vlastnosti `Author` v `books[0]` způsobí, že EF bude dotazovat databázi pro autora.</span><span class="sxs-lookup"><span data-stu-id="02f3f-132">When lazy loading is enabled, accessing the `Author` property on `books[0]` causes EF to query the database for the author.</span></span>

<span data-ttu-id="02f3f-133">Opožděné načítání vyžaduje více databázových cest, protože EF odesílá dotaz pokaždé, když načte související entitu.</span><span class="sxs-lookup"><span data-stu-id="02f3f-133">Lazy loading requires multiple database trips, because EF sends a query each time it retrieves a related entity.</span></span> <span data-ttu-id="02f3f-134">Obecně platí, že pro objekty, které jste serializováni, chcete zakázat opožděné načítání.</span><span class="sxs-lookup"><span data-stu-id="02f3f-134">Generally, you want lazy loading disabled for objects that you serialize.</span></span> <span data-ttu-id="02f3f-135">Serializátor musí číst všechny vlastnosti modelu, které aktivují načítání souvisejících entit.</span><span class="sxs-lookup"><span data-stu-id="02f3f-135">The serializer has to read all of the properties on the model, which triggers loading the related entities.</span></span> <span data-ttu-id="02f3f-136">Například zde jsou dotazy SQL v případě, kdy EF serializace seznam knih s povoleným opožděným načtením.</span><span class="sxs-lookup"><span data-stu-id="02f3f-136">For example, here are the SQL queries when EF serializes the list of books with lazy loading enabled.</span></span> <span data-ttu-id="02f3f-137">Můžete vidět, že EF vytvoří tři samostatné dotazy pro tři autory.</span><span class="sxs-lookup"><span data-stu-id="02f3f-137">You can see that EF makes three separate queries for the three authors.</span></span>

[!code-console[Main](part-4/samples/sample10.sql)]

<span data-ttu-id="02f3f-138">Existují i časy, kdy možná budete chtít použít opožděné načítání.</span><span class="sxs-lookup"><span data-stu-id="02f3f-138">There are still times when you might want to use lazy loading.</span></span> <span data-ttu-id="02f3f-139">Eager načítání může způsobit, že EF generuje velmi složité spojení.</span><span class="sxs-lookup"><span data-stu-id="02f3f-139">Eager loading can cause EF to generate a very complex join.</span></span> <span data-ttu-id="02f3f-140">Nebo možná budete potřebovat související entity pro malou podmnožinu dat a opožděné načítání by bylo efektivnější.</span><span class="sxs-lookup"><span data-stu-id="02f3f-140">Or you might need related entities for a small subset of the data, and lazy loading would be more efficient.</span></span>

<span data-ttu-id="02f3f-141">Jedním ze způsobů, jak zabránit problémům s serializací, je serializace objektů přenosu dat (DTO) místo objektů entit.</span><span class="sxs-lookup"><span data-stu-id="02f3f-141">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects.</span></span> <span data-ttu-id="02f3f-142">Tento postup budu zobrazovat později v článku.</span><span class="sxs-lookup"><span data-stu-id="02f3f-142">I'll show this approach later in the article.</span></span>

### <a name="explicit-loading"></a><span data-ttu-id="02f3f-143">Explicitní načítání</span><span class="sxs-lookup"><span data-stu-id="02f3f-143">Explicit Loading</span></span>

<span data-ttu-id="02f3f-144">Explicitní načítání je podobné opožděnému načítání s tím rozdílem, že explicitně získáte související data v kódu; k tomu nedochází automaticky při přístupu k navigační vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="02f3f-144">Explicit loading is similar to lazy loading, except that you explicitly get the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="02f3f-145">Explicitní načítání nabízí větší kontrolu nad tím, kdy načíst související data, ale vyžaduje další kód.</span><span class="sxs-lookup"><span data-stu-id="02f3f-145">Explicit loading gives you more control over when to load related data, but requires extra code.</span></span> <span data-ttu-id="02f3f-146">Další informace o explicitním načítání najdete v tématu [načítání souvisejících entit](https://msdn.microsoft.com/data/jj574232#explicit).</span><span class="sxs-lookup"><span data-stu-id="02f3f-146">For more information about explicit loading, see [Loading Related Entities](https://msdn.microsoft.com/data/jj574232#explicit).</span></span>

## <a name="navigation-properties-and-circular-references"></a><span data-ttu-id="02f3f-147">Navigační vlastnosti a cyklické odkazy</span><span class="sxs-lookup"><span data-stu-id="02f3f-147">Navigation Properties and Circular References</span></span>

<span data-ttu-id="02f3f-148">Když jsme definovali knihu a tvorbu modelů, definovali jsme navigační vlastnost pro třídu `Book` pro relaci typu kniha – autor, ale v druhém směru jsme nedefinovali vlastnost navigace.</span><span class="sxs-lookup"><span data-stu-id="02f3f-148">When I defined the Book and Author models, I defined a navigation property on the `Book` class for the Book-Author relationship, but I did not define a navigation property in the other direction.</span></span>

<span data-ttu-id="02f3f-149">Co se stane, když přidáte odpovídající navigační vlastnost do třídy `Author`?</span><span class="sxs-lookup"><span data-stu-id="02f3f-149">What happens if you add the corresponding navigation property to the `Author` class?</span></span>

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

<span data-ttu-id="02f3f-150">To bohužel při serializaci modelů vytvoří problém.</span><span class="sxs-lookup"><span data-stu-id="02f3f-150">Unfortunately, this creates a problem when you serialize the models.</span></span> <span data-ttu-id="02f3f-151">Pokud načtete související data, vytvoří se kruhový graf objektů.</span><span class="sxs-lookup"><span data-stu-id="02f3f-151">If you load the related data, it creates a circular object graph.</span></span>

![](part-4/_static/image1.png)

<span data-ttu-id="02f3f-152">Pokud se formátovací modul JSON nebo XML pokusí o serializaci grafu, vyvolá výjimku.</span><span class="sxs-lookup"><span data-stu-id="02f3f-152">When the JSON or XML formatter tries to serialize the graph, it will throw an exception.</span></span> <span data-ttu-id="02f3f-153">Tyto dva formátovací moduly vyvolávají odlišnou zprávu o výjimce.</span><span class="sxs-lookup"><span data-stu-id="02f3f-153">The two formatters throw different exception messages.</span></span> <span data-ttu-id="02f3f-154">Tady je příklad pro formátovací modul JSON:</span><span class="sxs-lookup"><span data-stu-id="02f3f-154">Here is an example for the JSON formatter:</span></span>

[!code-console[Main](part-4/samples/sample12.cmd)]

<span data-ttu-id="02f3f-155">Tady je formátovací modul XML:</span><span class="sxs-lookup"><span data-stu-id="02f3f-155">Here is the XML formatter:</span></span>

[!code-xml[Main](part-4/samples/sample13.xml)]

<span data-ttu-id="02f3f-156">Jedním z řešení je použití DTO, který je popsán v následující části.</span><span class="sxs-lookup"><span data-stu-id="02f3f-156">One solution is to use DTOs, which I describe in the next section.</span></span> <span data-ttu-id="02f3f-157">Alternativně můžete nakonfigurovat formátovací moduly JSON a XML pro zpracování cyklů grafu.</span><span class="sxs-lookup"><span data-stu-id="02f3f-157">Alternatively, you can configure the JSON and XML formatters to handle graph cycles.</span></span> <span data-ttu-id="02f3f-158">Další informace najdete v tématu [zpracování cyklických odkazů na objekty](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span><span class="sxs-lookup"><span data-stu-id="02f3f-158">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).</span></span>

<span data-ttu-id="02f3f-159">Pro tento kurz nepotřebujete `Author.Book` navigační vlastnost, takže ji můžete opustit.</span><span class="sxs-lookup"><span data-stu-id="02f3f-159">For this tutorial, you don't need the `Author.Book` navigation property, so you can leave it out.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="02f3f-160">[Předchozí](part-3.md)
> [Další](part-5.md)</span><span class="sxs-lookup"><span data-stu-id="02f3f-160">[Previous](part-3.md)
[Next](part-5.md)</span></span>
